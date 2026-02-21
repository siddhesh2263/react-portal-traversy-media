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

Note that when we are migrating code from the HTML page to the React components, we don't need the head section from those HTML pages. It will be handled by React.

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

For now, we will use a JSON file. Remove the { and the jobs: field, let it be from [. We now have an array of jobs.

Again, instead of passing it from App.jsx file, we will create a component that does the listing of the jobs, and then another component that holds data for one job.

Now, we will import the jobs.json in the JobListing component, and use the map function to list it out. We will later switch to JSON server.

Copy one of the job listing div, and paste it inside the map function (we will use it to iterate over the JSON jobs data.) Be sure to modify and not delete the wrong divs.

Now in JobListings component, we added the HTML and iterated over the JSON array. Let's put that in a separate component. Create a component called JobListing (previous one was JobListings.) This is how the updated JobListings component looks like:
```
const JobListings = () => {
  return (
    <section className="bg-blue-50 px-4 py-10">
      <div className="container-xl lg:container m-auto">
        <h2 className="text-3xl font-bold text-indigo-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {jobs.map((job) => (
                <JobListing job={ job }></JobListing>
            ))}
        </div>
      </div>
      </section>
  )
}
```
The job is passed as a prop to the JobListing component.

<br>

## States

There are 2 types of states:
- Component state, which relates to a single component, like the Navbar, HomeCards, etc.
- App level or global state, which relates to the entire app, and can be passed down to components.

We will look at components state.

In the JobListing, we want a button that says show more description, which is a toggle button. This component will have a piece of state called the showFullDescription, which can be changed when clicked on the button.

Below is the declaration for that state:
```
const [showFullDescription, setShowFullDescription] = useState(false);
```
Our state will have 2 values - true or false. By default, we want it to be false state. In the brackets:
- The first paramater is the name of that state,
- The 2nd param is the name of the function we call to change that state.

Below is how the function is used:
```
<button onClick={ () => setShowFullDescription((prevState) => !prevState) } className='text-indigo-500 mb-5 hover:text-indigo-600'>
    {showFullDescription ? 'Less' : 'More'}
</button>
```
When the button is clicked, it calls the function which changes the state. The prevState is the current state value that is set for that state (it can be named anything,) and we update that state value by setting it to opposite of the current value. Note that only that specific JobListing component will be affected.

<br>

## React icons

A small section where the location is present, we want to add an icon. Currently it's not visible. Run the command:
```
npm i react-icons
```
This will allow to work with Font Awesome, but also Material packages as well. We will use the following component:
```
<FaMapMarker className='inline text-lg mb-1 mr-1'></FaMapMarker>
```

<br>

## React Router

We want more pages in our application, but React doesn't provide routing by itself. Router is a separate package.
```
npm i react-router-dom
```

Create a pages folder under src, and create HomePage.jsx file.

This is the current code in App.jsx for router:
```
import React from 'react'
import { Route, createBrowserRouter, createRoutesFromElements, RouterProvider } from 'react-router-dom'
import HomePage from './pages/HomePage';

const router = createBrowserRouter(
  createRoutesFromElements(<Route index element={<HomePage></HomePage>}/>)
);

const App = () => {
  return (
    <RouterProvider router={ router }></RouterProvider>
  )
}

export default App
```

Now, we created the HomePage.jsx file, which is a simple React component:
```
import React from 'react'

const HomePage = () => {
  return (
    <div>HomePage</div>
  )
}

export default HomePage
```

As per my understanding, we set the index route which would be /, and set the element to be loaded as the HomePage component. Next, we initialized the router to be able to access that HomePage.

In the HomePage.jsx, we added the Hero component.

Now, the Navbar, the footer needs to be showed on every page. We will use layouts here.

<br>

## Layouts

1:24:41

Create a layouts folder. A project can have multiple layouts, but for this one we have 1. Create a MainLayout.jsx file, since it will be a component.
Now, import it in the App.jsx file.
Then, we need to create a parent route to the rest of our routes.

Any routes that are put in the MainLayout section, will use the MainLayout.
```
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path='/' element={<MainLayout></MainLayout>}>
      <Route index element={<HomePage></HomePage>}/>
    </Route>
)
```

Now in the MainLayout file, whatever route or page comes to this layout, will come through Outlet. Below is how it is used:
```
const MainLayout = () => {
  return (
    <>
        <Outlet></Outlet>
    </>
  )
}
```

Now we want the Navbar to be shown on every page, so we will put that in this layout file. This is done like so:
```
const MainLayout = () => {
  return (
    <>
        <Navbar></Navbar>
        <Outlet></Outlet>
    </>
  )
}
```

Below is the image how it will be displayed:

<p align="center">
  <img 
    src="https://github.com/siddhesh2263/react-portal-traversy-media/blob/main/assets/003-layout-navbar-home.png?raw=true"
    alt="Layout Navbar Home"
    width="400"
  />
</p>

Now currently in the HomePage.jsx file page, we just have the Hero section. Add the HomeCard component below it, like so:
```
const HomePage = () => {
  return (
    <>
        <Hero></Hero>
        <HomeCards></HomeCards>
    </>
  )
}
```

So now instead of putting all this in the App component, we are putting it in the HomePage.

<br>

## Jobs page and Jobs route

So here's the general flow what would be - we add a page, and then we add the route for that page in the App.jsx file.

Create a JobsPage.jsx file, as a React component. Now, we add the route, like so:
```
<Route path='/' element={<MainLayout></MainLayout>}>
  <Route index element={<HomePage></HomePage>}/>
  <Route path='/jobs' element={<JobsPage></JobsPage>}/>
</Route>
```

We won't use a tags, but will use links. Update all the .html href to just /, /jobs, and /add-job in the Navbar component.

We don't want to use a tags because it does a complete page refresh. With a link tag, it doesn't do a refresh. We need to import Link from the react-router-dom library. So, change a tag to Link, and the href to `to`. All these changes are in the Navbar component. Now, there is no page refresh, because it is on the client.

These changes are to be done in the HomeCards component.

Now, the changes are to be done in the JobListing component.

Now, changes in the ViewAllJobs.

Below is one of the changes how it's done:
```
const ViewAllJobs = () => {
  return (
    <section className="m-auto max-w-lg my-10 px-6">
        <Link
            to="/jobs"
            className="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        >View All Jobs</Link>
    </section>
  )
}
```
The a tag to Link, and href to `to`.

<br>

## Custom 404 page

Create a new page called NotFoundPage.jsx. Copy the section code from the HTML page. Rename class to className, and a tag to Link, href to `to`.
Since this page has icons, import the icons component.

Now to make this page show on routes that are not present, go to App component. Add a route, and this is how it's done:
```
<Route path='*' element={<NotFoundPage></NotFoundPage>}/>
```
This means that catch all the routes that are not defined in the Router, to show this NotFoundPage component.

Below is how the custom page would look:
<p align="center">
  <img 
    src="https://github.com/siddhesh2263/react-portal-traversy-media/blob/main/assets/004-page-not-found.png?raw=true"
    alt="Page Not Found"
    width="400"
  />
</p>

## Highlight active Navbar

Now, see that in the Navbar, we want to highlight the nav buttons in black only on those pages where it is currently on. So the Home button needs to be active when on home page, Jobs for jobs, etc.

These changes are to be done in Navbar component.

Change all instances of Link to NavLink. NavLink adds a class to the active link. Now, we need to use that class to set the styling for the links, like so:
```
<NavLink
  to="/"
  className={({ isActive }) => isActive ? 'bg-black text-white hover:bg-gray-900 hover:text-white rounded-md px-3 py-2' : 'text-white hover:bg-gray-900 hover:text-white rounded-md px-3 py-2'}
  >Home</NavLink>
<NavLink
```
If the link isActive is true, which it will be when it's on the home page, it will have a black background. Otherwise, it won't.

Instead of having this for all the links, we will create a function at the top, and then use it for the individual links:
```
// Function:
const linkClass = ({ isActive }) => 
    isActive ? 'bg-black text-white hover:bg-gray-900 hover:text-white rounded-md px-3 py-2' : 'text-white hover:bg-gray-900 hover:text-white rounded-md px-3 py-2'
  
// Usage in indivisual links:
<NavLink
  to="/add-job"
  className={linkClass}
  >Add Job
</NavLink>
```

<br>

## Jobs page

In the JobsPage page, import the JobListings component, which loads all the jobs from the JSON file. But now the problem is, only 3 are shown, because we used slice. We will use a prop in the JobListings component called isHome, which by default is set to false.

Now we are passing this JobListings component from the HomePage page. Over here, add the prop of isHome. So, final changes in HomePage page are as follows:
```
const HomePage = () => {
  return (
    <>
        <Hero></Hero>
        <HomeCards></HomeCards>
        <JobListings isHome={ true }></JobListings>
        <ViewAllJobs></ViewAllJobs>
    </>
  )
}
```

Below is the final changes in the JobListings component, where the isHome prop is passed:
```
const JobListings = ({ isHome = false }) => {
    const jobListings = isHome ? jobs.slice(0, 3) : jobs;
  return (
    <section className="bg-blue-50 px-4 py-10">
      <div className="container-xl lg:container m-auto">
        <h2 className="text-3xl font-bold text-indigo-500 mb-6 text-center">
          { isHome ? 'Recent Jobs' : 'Browse Jobs' }
        </h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {jobListings.map((job) => (
                <JobListing key={ job.id } job={ job }></JobListing>
            ))}
        </div>
      </div>
      </section>
  )
}
```

<br>

## JSON server setup

1:44:10

We will use json-server. Install it:
```
npm i -D json-server
```

Configure the command in the package.json file, under the scripts section:
```
"server": "json-server --watch src/jobs.json --port 8000"
```

Run the command:
```
npm run server
```

This gives the path where the jobs json data is hosted, as seen in the image:
<p align="center">
  <img 
    src="https://github.com/siddhesh2263/react-portal-traversy-media/blob/main/assets/005-json-server.png?raw=true"
    alt="JSON Server"
    width="400"
  />
</p>

It is at `http://localhost:8000/jobs`. Now in the browser we can access a particular job by passing the ID, like `http://localhost:8000/jobs/1`.

Now, we need to be able to fetch this data, and this is done from the JobListings component. This component is being used in the HomePage and the JobsPage. We no longer will be using the job files, but will be making a request. We will be doing that inside of a useEffect hook.

<br>

## useEffect hook

The useEffect hook allows the components to have side effects. We want a side effect of fetching the data when the component renders. And when we get those jobs from the API, we want to put them in state, so we also want to bring in useState.

We defined state like this:
```
const [jobs, setJobs] = useState([]);
```
The default value for jobs is going to be an empty array. We will make a request when the component loads through the useEffect, and then we will fill this empty array with the response from the API.

We will also pass a loading state, which will show loading when the data is being fetched:
```
const [loading, setLoading] = useState(true);
```
The default will be true, meaning data is being loaded, and then set to false once data fetched.

Now we will define the useEffect. It takes 2 parameters:
- A function,
- A dependency array

We want to have an empty array in most cases. What that means is when the value changes inside that array, it will call the function, i.e this useEffect will run. You want to have an empty array in there, otherwise it will run as a never ending loop.

We need to create a separate async function inside of it.

We will briefly understand the below code section:
```
const [jobs, setJobs] = useState([]);
const [loading, setLoading] = useState(true);

useEffect( () => {
  const fetchJobs = async () => {
    try {
      const res = await fetch('http://localhost:8000/jobs');
      const data = await res.json();
      setJobs(data);
    } catch (error) {
      console.log('Error fetching data', error);
    } finally {
      setLoading(false);
    }
  }
  fetchJobs();
}, []);
```

There are 2 states - for job, and for loading. Now, the above code shows how asynch and await can be used inside of useEffect hook. A request is made to the json server, and once the data is received, it is stored in the jobs state, using the setJobs useState hook. If any error it is presented in logs. Then, since finally is anyways run, it will update the loading state. In this way now, the UI is able to load the listings from an API.

We add the loading component just before it is rendered.

1:54:14

<br>

## Loading spinners

Install the below package:
```
npm i react-spinners
```

Create a component called Spinner.jsx under components folder. Below is the Spinner component code:
```
const override = {
    display: 'block',
    margin: '100px auto'
}

const Spinner = ({ loading }) => {
  return (
    <ClipLoader 
        color='#4338ca'
        loading={loading}
        cssOverride={override}
        size={150}
    >
    </ClipLoader>
  )
}
```
It uses ClipLoader component, and we need to pass the loading as a prop from the JobListings component. CSS override is to override the style with custom styling. Changes need to be done in JobListings component, like so:
```
<div className="grid grid-cols-1 md:grid-cols-3 gap-6">
    {loading ? (<Spinner loading={loading}></Spinner>) : (
      <>
        {jobs.map((job) => (
          <JobListing key={ job.id } job={ job }></JobListing>
        ))}
      </>)
    }
</div>
```
The Spinner component is imported and used here.

We can see the spinner for a quick instance, but it is not in the middle. This is because of the grid. Instead, use that grid classname div inside the jobs.map conditional, rather than keeping it outside.

<br>

## Homepage reduced listings

Initially we had 3 listings in HomePage, and all of them in JobsPage. However, now it's showing all of them again in HomePage. We can work around this, sincce we have the isHome prop available to us. We need to make changes in the useEffect hook.

Use of ternary operator to use multiple URLs:
```
const apiUrl = isHome ? 'http://localhost:8000/jobs?_limit=3' : 'http://localhost:8000/jobs';
```

As of now, he _limit=3 seems to be deprecated, and does not work. We will display all jobs in the HomePage as of now.

<br>

## Creating a proxy

Changes are done in the vite.config.js file, where the below config is added:
```
export default defineConfig({
  plugins: [react(), tailwindcss()],
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      }
    }
  }
})
```

So when we hit /api/jobs, it is going to hit localhost/jobs.

Make changes in the JobListings component:
```
const apiUrl = isHome ? '/api/jobs?_limit=3' : '/api/jobs';
```

2:01:00

<br>

