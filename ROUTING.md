# Routing

## Frontend routing

The project for the frontend uses Next.js default routing. You can find more information about Next.js routing in the [Next.js documentation](https://nextjs.org/docs/routing/introduction).

For a new route in the frontend, you need to create a new file in the `src/pages` folder. For example, if you want to create a new route `/about`, you need to create a file `src/pages/about.tsx`. Then, you can access the route at `http://localhost:3000/about`.

## Backend routing

For the backend, we use Express.js as the web framework. You can find more information about Express routing in the [Express documentation](https://expressjs.com/en/guide/routing.html).

Instead of putting all the routes in the same file (in our case, it's `app.ts`), we split the routes into different files. All the routes are in the `src/routes` folder.
