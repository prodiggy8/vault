**Parnas:** Module should be designed to hide secrets that are likely to change; interface should be unlikely to change.

Language-specific ways to enforce: libraries, private classes.

Professor building his startup: Scala & Heroku, needed simplicity for deployment

No such a thing as an interpreted or compiled language: there's just what is common. PHP now has  JIT; you could write an interpreter for C++.

What does stateless really mean? Apps have sessions, shopping carts, etc.
- You can have a stateless service and then a stateful service that encapsulates it!
- All depends on memory: current state is independent of past.
- Even client can store the state for me! And pass it on every request.

**AI impact:** developers are doing more reviews, design, SRE work

Code reviews on avalanche of AI generated code? AI reviewing? Static analysis? Gain confidence?
- More tools: more of all of them, more proofs about code