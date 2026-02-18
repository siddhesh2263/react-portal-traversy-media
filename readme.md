# React Portal

Frontend for a job listing website.

React is a JS library to build user interfaces.

Angular is a framework. React is a UI library.

Ecosystem of React is huge - can be used for SPA, SSR pages, and static pages.

Ajax was used to get server from data without having to refresh the page. This allowed to build SPA. WHen it grows, it can be hard to maintain. This is where React comes in, to build large scale UI. Vanilla JS usage for this can be messy.

React uses something called the virtual DOM (document object model.) This is a lightweight copy of the actual DOM. When the state of a component changes, the virtual DOM changes first, and then React will compare the virtual DOM and the actual DOM, and it will update the parts than needed to be updated. This is how tradionally React works (at least version 18.) React 19 as  per the author will not use the virtual DOM, but will use a compiler, which will improve performance.

<p align="center">
  <img 
    src="https://github.com/siddhesh2263/react-portal-traversy-media/blob/main/assets/001_dom_compare.png?raw=true"
    alt="DOM Compare"
    width="400"
  />
</p>

As per the author, Vue JS and Swell do things in a lot more straighforward way.

## Components
They are reusable piece of code that can be used to build elements on a page. They can be thought as custom HTML elements. This allows to break down complex UIs into smaller, manageable pieces, and makes code easier to maintain and scale. We will be using functional components in this project. Components can take in props, that are arguments or attributes. They can hold their own state.

## State
This represents the data that a component manages internally, and could be used in form input data, fetched data, and UI-related data. To define state in a functional component, we can use hooks. useState hook is used for this. This function will return an array with 2 elements: the current state value, and the function to update that state. There is also global state. For instance, when the data from a database needs to be shared among all components.

## Hooks
React hooks are functions that enable functional components to use state and other React features without writing a class. React used to have classes, and these classes had life cycle methods, which were methods that ran at specific times during the component rendering process. Functional components don't have a lifecycle methods, because they are not a class, so hooks allows us to do the same work which the life cycle methods used to do, such as fetch state, or perform data fetching, etc. useState and useEffect are 2 important hooks. All hooks start with the word use, and you can also create custom hooks within your components, which basically can do anything.

## JSX (JavaScript Syntax Extension)
Components have state associated with it (which just means what data they have,) and it can also take in props. JSX is returned from a React component, and it is HTML-like syntax within JavaScript. JSX is dynamic, and it is what HTML would be if it were a programming language. JSX can have loops, conditionals, etc. There are slight differences in naming.

## SPA, SSR, and SSG
SPA (single page app) loads a single HTML file and a JS bundle, which loads the entire UI. So when a route is hit, it does not go to server, but JS loads that content. SPA are good for fast, dynamic pages. Can have issues with SEO.
SSR (server side rendered) - In this, the server sends the fully rendered page to the client. They still use React. Instead of being bundled in JS, the initial page is loaded from the server, which can be good for SEO and initial page load time. SSR needs a server to run (Vercel, Netlify.)
SSG (static site generation) - Gatsby generates static HTML files at build time (ex: Gatsby.)

We will be using Vite.

---

20:02