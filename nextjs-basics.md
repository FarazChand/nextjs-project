# NextJS Basics

- the traditional vite/react focus almost entirely on the front end
  - still need a seperate backend app like nodeJS to do things like update a database
- server side allows us do to more computational heavy tasks, use api keys, interact with a database
- a Next JS app has a client side and a server side, its a full stack framework
- it uses "server components" and "client components"

### Server Components

- server components allow you to do things like fetch data and other traditional backend tasks
- it will render the component in the backend and then send that to the client side
- all next js components are server components by default

### Client Components

- render in the browser
- used when you need to hook into browser events
- e.g. a user clicks on a button
- also needed when using react hooks like useEffect, useState etc
- if you want a component to be a client component you need to explicitly state it at the top of the file stating "use client"

### Server Actions

- used for updating data e.g. add a new post, edit a post or delete post
- functions that run only on the server side but can still be triggered from the browser
- e.g. you submit a post, the data from the browser goes to the designated server function which will take your data and update your database
- traditionally you would use api endpoint for that

### route handlers (API)

- GET , POST, PUT api endpoints
- you have to manually send the data from the browser to the api endponts
- many times we might prefer using server actions instead
- however there are cases you would want to use route handlers
  - web hooks (e.g. stripe, someone pays and stripe send information about the transaction. You need a place they can send it too)

  ## Creating a NextJS app:

  ```
  npx create-next-app@latest
  ```

- will start the creation of a nextjs app in the directory you are currently in
- say yes to version
- name app
- use the recommended defaults
  - uses app router, tailwind, typescript, eslint

### Default Project Files

- you will see config files from your .gitignore all the way to the bottom
  - tsconfig.json -> configs for typescript
  - postcss.config.md -> used by tailwind
  - eslint.config.mjs -> linter
  - next.config.ts -> configs for nextjs itself
  - README.md -> quick description of what the app is doing
  - package.json -> description of our project, specifies dependencies
  - package-lock.json -> shows full tree of dependencies
  - .gitignore -> for data we dont want to upload to github e.g. env variables
  - AGENTS.md
  - CLAUDE.md -> AI coding agents

  Above the config files are the project directories:
  - next/types -> nextjs refers to this
  - node_modules -> where the packages are installed
  - public -> for static files like images, videos, pdfs
  - app -> where your application lives (think src in vite/react)

### App Directory

- page.tsx
  - the homepage
  - page.tsx is a special name that specifies this file as the home/main page of its directory
  - what ever we render here will be displayed on the root of the domain

- layout.tsx
  - wraps all pages
- globals.css -> styling
- favicon.ico -> the icon of the app

## Running your NextJS App

```
npm run dev
```

- can find this command in package.json (next dev -> note that we only used the "dev" part)
- you can also ask your ai agent to do this
- make sure you are in the root of your project directory when you run this command

## AI Specific Updates

- we have seen that there is an AGENTS.md and a CLAUDE.md file
  - these are for your AI coding agents
  - Claude code will automatically look for CLAUDE.md in your project
  - other coding agents will look for AGENTS.md
  - CLAUDE.md file refers to the AGENTS.md file, so we can just put everything in the AGENTS.md file
  - these are basically instructions for your coding agents
    - models are often trained on older data
    - nextjs has tricky/subtle parts to it that coding agents often get wrong
    - so you will see some default instructions that allow for the coding agent to update its knowledge on current next js docs
    - you will see the instructions direct the agents to "node_modules/next/dist/docs/"
    - this is in our project and we can visit this ourselves to see what information the agents will be consuming
    - essentially, the agents do not have to go outside of the app to get the standard way of using your current version of nextjs used in the app
    - the information here is actually very useful and would be a great read for deeper and complete understanding of nextjs in its current state

### Browser Log Forwarding

- as you are developing your app, there may be client side errors
- previously you would have to go into your browser console, copy them, and give them to your AI coding agent
- instead now you can enable in the next.config.js a browser to terminal option
  - https://nextjs.org/blog/next-16-2-ai#browser-log-forwarding

### Running your AI agent (Requires billing to Claude or Codex)

- you need to run the agent in the terminal, it needs to start the dev server itself
- end your dev server connection if its running and run claude
- can say "start dev server"
- it will run npm run dev for you
- dev server will be running, but it will be managed by claude
- now if there are errors, claude will be notified because it has access to the output of that dev server

#### Managing AI Coding Agents dev server creation

- ai coding agents seem to be eager to start new dev servers
- .next/dev/lock
  - this lock file describes which dev server is currently running
  - if your agent tries to start a new dev server, next js will give it information about the current one that is currently running
  - this should help with your agents managing those dev servers for you

#### Experimental Agent Dev Tools:

- will dive into this later on \*\*

### Free local Agent:

- if you dont have the money to access claude code, there are some free options
- these require some set up, I also don't know how trust worthy these are
- need to explore this in the future, here are 3 options:
  1. Redirect Claude Code to Free AI Backends
  2. Use "Free Claude Code" Open-Source Wrappers
  3. Free Local Agents (Ollama)

We are probably not going to dive into agent usage for this application but its good to know about it.

## Project Start

### Changing Project Title and Description

- this referes to the text on the tab at the top of the page in the browser that represents the website
- these show up on google search rankings, ai apps may use this information if the website is asked about
  - go to app/layout.tsx
  - find the "metadata" object
  - change the "title" attribute to the desired title value
  - can also change the "description" attribute

### Cleaning up Homepage

The nextjs application will start with a lot of boiler plate. We want to clean this up before we start working on our app:

- go to app/page.tsx
- clean up the component by removing all of the elements within the return

- go to layout.tsx
- adjust the styles you want to wrap every page component

### Understanding layout.tsx

- this layout wraps every single page
- it works exactly the same as in react:
  - you have a parent component
  - in between the opening and closing tags you have the "children" prop
  - the children would be the pages that this layout wraps
  - next renders every page within this layout

- this is powerful because you can navigate to different pages, and non of the layout will change
- header and footer can be part of your layout.tsx, and thus will not change
- but the page content itself will change

### Header and Navigation

- the basic semantic html tags all exist, same as react:
  - Header, Footer, Nav

#### Link Component

- traditionally in HTML you would use an anchor tag <a> with an href
- when a user clicks on this it would request a whole html page form the server aka "hard navigation"
- in nextjs we have the "Link" component
  - only swaps out the part it needs to rerender
  - the header and footer stay the same
  - aka "soft navigation", feels smoother to the user

  - has an href that can point to the desired route e.g. "/", "/post" etc
  - you will render the page.tsx of that particular route e.g. app/page.tsx, app/posts/page.tsx

  - also does something called pre fetching
  - any links in view will be pre-fetched
    - this means the components will be rendered and sent to the client before the user even clicks on the link
    - this makes the content appear very fast for the user
    - by default this is only enabled in production, not in a dev server
  - typically you want to keep this enabled, however you can disable it if it makes sense
    - e.g. if a footer has hundreds of links that people might not click on often, it can be wasteful to prefetch all of the content for those links
    - do this by setting the prefetch attribute to false

### Creating a new page route

- we create a new directory named after the route we want to create, e.g. app/posts
- we then create a page.tsx file for that route
- the standard naming convention for the component inside the route will be the name of the route Capitalized, followed by "Page" e.g. PostsPage (might be required to name this way not sure)
- obviously it is a component so we have to structure it the same way a component is structured in react
- this page.tsx is going to be the content rendered within the app/layout.tsx when this route is navigated to (either through a Link tag or through url e.g. http://localhost:3000/posts)

### Image component

- traditionally in html you would use the plain image tag <img /> which we can still use in nextjs if we want to
- nextjs has a dedicated Image component, which comes with a bunch of optimization options out of the box:
  - can specify width and height through attributes, which helps prevent content shifting with bigger images
  - can create bigger and smaller versions of your image, depending on the device of the user - faster and overall better performance for you images
  - src attribute allows you to link internal images in project or external images through url
    - in older versions of nextjs, you would get a warning when linking external images - and you would have to allow it through next config files

Note: Can wrap Image components in Link components - e.g. for the header logo you would expect clicking that image would lead you to the home page.

## Creating Reusable Custom Components

Similar to react, we might not want to clutter our layout or homepage with too much jsx. We also might want to use a component from one page on multiple other pages. We can abstract components into their own files and import them where needed, only needing to insert their tag into the location we want to use them.

- its a standard practice to create a components folder for this
  - /app/components
    -> this is one option, works fine
  - /components
    -> if you want the app directory strictly for routes
    -> its totally fine to have another directory within your root project directory, your project structure is up to your preference

- the name for the component file would be lowercase, .tsx file
- export default, allows for cleaner imports. Though not required to do
- the function name would be the same as the file name, but capitalized
  - e.g. for a Header component.
  - you would keep it in /components/header.tsx

  ```
      export default function Header() {
          ...your header code here...
      }
  ```

## Data Fetching in Server Components:

- in a client side only react/vite type of application, you would have some kind of "useEffect" which would make an API call, the API would send back some data.
- this is still possible in nextjs using client components

- however, typically in NextJS - we are going to fetch data directly from the server side.
  - we can do this using server components
  - the server component fetches data from the API directly
  - the data is sent back to the server component
  - the server component uses this data to render the component server side
  - the rendered component is then sent to the client side and displayed in the browser

- we need to add the async keyword to the function signature
- then we can just await fetch as usual, .json the response and map the data inside our component
- one benefit is being able to use api keys directly in the server component since it isnt exposed to the client - only the rendered result is. However, if this is a public github project its probably best to not expose the api in any component that will be stored in public view. But its worth noting

## Dynamic Routes

- we might have a page route that leads to a page with a bunch of items a user can click on e.g. posts, with post items on the page
- we would probably want each post item to lead to its own post page once clicked
- we can do that with nextJS by using dynamic routes
  - we create a directory within our app/posts directory, but we name it [id] -> app/posts/[id]
  - the name within the brackets is optional, it is a variable that we use in the page component of that directory
  - it represents the url endpoint of the post in this case, which we can use to fetch/specify data that we want to display from the posts array
  - that being said, app/posts/[id]/page.tsx should be created, which is where we are going to store our dynamic component
  - this component is dynamic because it will have a general layout, but the content will differ depending on the endpoint of the url.
  - so if we think about our app/posts page, that page has a bunch of post items. Each post item is a Link that leads to a url with that post's id as the end point.
  - then that post id is used to either fetch the post itself, or used to find the post within the already fetched posts array (depends on how the data is stored)

TODO : Make sure you go over dynamic routes and params, typing of params and how to use it thoroughly because its a really important topic
