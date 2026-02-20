# React Portal

## (in development)

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

<br>

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

Below is the project homepage:
<p align="center">
  <img 
    src="https://github.com/siddhesh2263/react-portal-traversy-media/blob/main/assets/002-home-page.png?raw=true"
    alt="Home Page"
    width="600"
  />
</p>

<br>

## Development Notes

Create the project:
```
npm create vite@latest react-portal
```
Choose:
React, JavaScript.

In the vite.config.js file, update port:
```
// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  }
})
```

Install dependencies:
```
npm install
```

Run the application:
```
npm run dev
```

In the index.html file, which is the HTML for the landing page, it has the following:
```
<body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
```
The root div is the starting point for generally UI frameworks/libraries, and then in the src folder, there is a main.jsx file, which is the entry point for the React application.

In the below main.jsx code section, it gets that root div from the index.html file we saw earlier, and uses the React components in it:
```
createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

The StrictMode checks if anything is deprecated, if any unsafe lifeycle methods are present, context API usage stuff like that.

Delete App.css file.

Install the ES7 extension.

Set up Tailwind (refer docs)

## JSX Recap

Every React component is going to return JSX. We can only return a single element, but can have as many elements inside it:
```
const App = () => {
  return (
    <div className='text-5xl'>App</div>
  )
}
```

Incorrect:
```
const App = () => {
  return (
    <div className='text-5xl'>App</div>
    <p>Another element</p>
  )
}
```

Correct usage:
```
const App = () => {
  return (
    <div>
      <div className='text-5xl'>App</div>
      <p>Another element</p>
    </div>
  )
}
```

It has to be wrapped in a single element. We can use fragments as well (empty HTML tags) like `<></>` instead of `<div></div>`.

We can use expressions, or variables inside the JS file, like so:
```
const App = () => {
  const name = 'Sid';
  const x = 10;
  const y = 20;
  return (
    <div>
      <div className='text-5xl'>App</div>
      <p>Hello { name }</p>
      <p>The sum of { x } and { y } is { x + y }</p>
    </div>
  )
}
```

We can also loops, and render a list.
```
const App = () => {
  const name = 'Sid';
  const x = 10;
  const y = 20;
  const names = ['S', 'C', 'V', 'X'];
  return (
    <div>
      <div className='text-5xl'>App</div>
      <p>Hello { name }</p>
      <p>The sum of { x } and { y } is { x + y }</p>
      <ul>
        { names.map((name) => (
          <li>{ name }</li>
        )) }
      </ul>
    </div>
  )
}
```

The array gives a warning - Each child in a list should have a unique key prop. If it were an object, we could have used the object ID. Since this is an array, we can use the index instead:
```
<ul>
  { names.map((name, index) => (
    <li key={ index }>{ name }</li>
  )) }
</ul>
```

We can use conditionals in JSX:
```
const App = () => {
  const name = 'Sid';
  cosnt loggedIn = true;

  return (
    <div>
      <div className='text-5xl'>App</div>
      <p>Hello { name }</p>
    </div>
    { loggedIn ? <h1>Hello Member</h1> : <h1>Hello Guest</h1> }
    { loggedIn && <h1>Hello Member</h1> }
  )
}
```

JSX is what HTML would be.

For styling, naming is used differently. Inline CSS can be used.
```
const App = () => {
  return (
    <div>
      <div className='text-5xl'>App</div>
      <p style={{ color: 'red', fontSize: '24px' }}>Another element</p>
    </div>
  )
}
```
So, font-size in CSS usage would be fontSize here in JSX.

We can store these styles in a variable as well:
```
const App = () => {
  const styles = {
    color: 'red',
    fontSize: '55px'
  }
  return (
    <div>
      <div className='text-5xl'>App</div>
      <p style={ styles }>Another element</p>
    </div>
  )
}
```

But in this project we won't be doing this because we will be using Tailwind, so we will be adding classes.

<br>

## Development Notes contd.

Ctrl Shift L to change multiple instances at once. Change class to className.

Create a components folder. Create Navbar.jsx file.
We moved the nav tag section into the Navbar.jsx file. Navbar.jsx was imported in App.jsx.
Import the logo image from the assets folder:
```
import logo from '../assets/images/logo.png';
```
Update the src for that image div.

Do the same thing for Hero section.

We will discuss props. In the Hero section, we are using a title and a subtitle. Let's pass it through App.jsx:
```
<Hero title='Test title' subtitle='This is the subtitle'></Hero>
```
Now in the Hero.jsx file, we will use props to destructure the passed variables:
```
const Hero = (props) => {
  ...

Usage:
<div className="text-center">
  <h1
    className="text-4xl font-extrabold text-white sm:text-5xl md:text-6xl"
  >
    { props.title }
  </h1>
  <p className="my-4 text-xl text-white">
    { props.subtitle }
  </p>
```

Or we can destructure as:
```
const Hero = ({ title, subtitle }) => {
  ...
```

We can have default props:
```
const Hero = ({ 
  title = 'Become a React Dev', 
  subtitle = 'Find the React job that fits your skill set', 
}) => {
  ...
```

Now moving on, there is a card section - for developers, and for employers. In the App.jsx file, we can use a Card component, and put the individual card content through the App.jsx file. However, we want to keep the App.jsx file clean, so we will create a wrapper component to hold these cards instead. We will call this component HomeCard. Create a HomeCard.jsx file.

Now as discussed earlier, we will create individual Card component.

Here's what's happened:
```
const Card = ({ children, bg = 'bg-gray-100' }) => {
  return (
    <div className={`${bg} p-6 rounded-lg shadow-md`}>
        { children }
    </div>
  )
}
```
This is the structure in the Card component. Now this Card will be used in the HomeCards component, like so:
```
const HomeCards = () => {
  return (
    <section className="py-4">
      <div className="container-xl lg:container m-auto">
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
          <Card>
            <h2 className="text-2xl font-bold">For Developers</h2>
            <p className="mt-2 mb-4">
              Browse our React jobs and start your career today
            </p>
            <a
              href="/jobs.html"
              className="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
            >
              Browse Jobs
            </a>
          </Card>
          <Card bg='bg-indigo-100'>
            <h2 className="text-2xl font-bold">For Employers</h2>
            <p className="mt-2 mb-4">
              List your job to find the perfect developer for the role
            </p>
            <a
              href="/add-job.html"
              className="inline-block bg-indigo-500 text-white rounded-lg px-4 py-2 hover:bg-indigo-600"
            >
              Add Job
            </a>
          </Card>
        </div>
      </div>
    </section>
  )
}
```
What this indicates is that the children used as props in the Card component will wrap the whole div that was used in the original HTML file. Now, we can add more props to this Card by passing style variables, such as to control the background in this case.

<br>

Now we are on the Browse Jobs section. Here, we will use JSON data to load this data.

55:32