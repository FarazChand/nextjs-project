# NextJS Basics

- the traditional vite/react focus almost entirely on the front end
  -- still need a seperate backend app like nodeJS to do things like update a database
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
  -- web hooks (e.g. stripe, someone pays and stripe send information about the transaction. You need a place they can send it too)

  ## Creating a NextJS app:

  ```
  npx create-next-app@latest
  ```
