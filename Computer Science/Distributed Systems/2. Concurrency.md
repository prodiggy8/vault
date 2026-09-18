---
tags:
  - distributed-systems
  - computer-science
  - course/15-440
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Saturday, September 5th 2026, 1:35:11 pm
date modified: Saturday, September 5th 2026, 1:35:20 pm
---
**Desired properties:**
- One process at a time in critical section
- Requests to enter critical section eventually succeed
- Access/delay to access is equitable
- Don’t waste resources

#### Semaphores

`V(x)` stands for verhogen, Dutch for “to increase”
`P(x)` stands for prolaag, Dutch for “try to reduce”

### FIFO Queue

With mutex, `Remove()` will not wait for an element if the queue is empty.
```go
func (q *Queue[T]) Remove() T {
	q.m.Lock()
	defer q.m.Unlock()
	var result = q.items[0]
	q.items = items[1:]
	return result
}
```

With a loop. This will not allow anyone to insert if the queue is empty.
```go
for {
	q.m.Lock()
	if len(q.items > 0) {
		// get item
	}
}
```

With semaphores, we keep the lock and use the semaphore to indicate the quantity. Now remove calls `P(x)` *before* keeping the lock needed by insert.
```go
q.s.P()
q.m.Lock()
// remove
q.m.Unlock()
return result
```

But then `Flush` breaks, it takes the lock but never touches the semaphore. The attempt below is a race condition, we unlock before finishing up.

Even if we clear the semaphore before, `P()` blocks and blocking while holding the lock is not good. Only a fraction of `V()` might have arrived.
```go
func (q *Queue[T]) Flush() {
	q.m.Lock()
	var n = len(q.items)
	q.items = nil
	q.m.Unlock()
	for i := 0; i < n; i++ {
		q.s.P()
	}
}
```

We go back the to the previous `Flush` and add a condition to `Remove()` to account for unsynced semaphore with regards to the count. 
```go
for {
	q.s.P()
	q.m.Lock()
	if len(q.items) == 0 {
		q.m.Unlock()
		continue
	}
	// remove
}
```

We can also use condition variables. For many implementations of `Wait` the below is a race condition. `Wait` does not guarantee the condition is true by the time `Remove` gets the lock.
```go
func (q *Queue[T]) Insert(x, T) {
	q.m.Lock()
	q.items = append(q.items, x)
	q.cond.Signal()
	q.m.Unlock()
}

func (q *Queue[T]) Remove() T {
	q.m.Lock()
	if len(q.items) == 0 {
		q.cond.Wait()
	}
	// remove
}
```

# Go

Now using proper Go.
```go
type Queue[T any] struct {
	in chan T
	out chan T
	flush chan chan struct{}
}

func (q *Queue T) Insert(x T) {
	q.in <- x
}

func (q *Queue T) Remove() {
	return <-q.out
}

func (q *Queue T) Flush() {
	ack := make(chan struct{})
	q.flush <- ack
	<-ack
}

func New[T any]() *Queue[T] {
	// makes q
	
	go func() {
		var items []T
		for {
			var outChan chan T
			var nextVal T
			if len(items) > 0 {
				outChan = q.out
				nextVal = items[0]
			}
		
			select {
			case item := <-q.in:
				items = append(items, item)
			case outChan <- nextVal:
				var zero T
				items[0] = zero
				items = items[1:]
			case ack := <-q.flush:
				items = nil
				ack <- struct{}{}
			} // end of select
		} // end of loop
	}() // end of routine
}

```