Next.js is a **React** framework
- Handles tooling and configuration needed for React
- Provides additional stuff

How browsers interpret code?

- Server returns HTML code
- Browser constructs a Document Object Model (DOM)
![[Pasted image 20251014200743.png]]
- JavaScript allows to manipulate DOM within the client
- Using JavaScript manipulation is verbose

### React

Pure JavaScript is imperative (**how** to do)
React is declarative (**what** to do)

React uses **JSX**, an extension for JavaScript that lets people use HTML-like syntax
- To render JSX, we need a compiler such as Babel

##### Core concepts:
1. **Components**

Self-contained and reusable snippets of code
Components are just JavaScript **functions** that return JSX
- Components functions need to be **capitalized**
- Components need to be referred to with **tags** like in HTML

```
function Header() { return <h1>Header</h1>; }
root.render(<Header />);
```

They can also be **nested**

```
function HomePage() { <div> <Header /> </div>; }
```


- **Props**
- **State**
