# NextJS Basics

- the traditional vite/react focus almost entirely on the front end
  - still need a seperate backend app like nodeJS to do things like update a database
- server side allows us do to more computational heavy tasks, use api keys, interact with a database
- a Next JS app has a client side and a server side, its a full stack framework
- it uses "server components" and "client components"

### Server Components

- server components allow you to do things like fetch data and other traditional backend tasks
- it will render the component in the backend and then send that to the client side

### Client Components

- render in the browser
- used when you need to hook into browser events
- e.g. a user clicks on a button
- also needed when using react hooks like useEffect, useState etc

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

### Free local Agent:

- if you dont have the money to access claude code, there are some free options
- these require some set up, I also don't know how trust worthy these are
- need to explore this in the future
  - Redirect Claude Code to Free AI Backends
  - Use "Free Claude Code" Open-Source Wrappers
  - Free Local Agents (Ollama)
