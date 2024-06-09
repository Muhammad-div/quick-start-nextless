# Testing strategy

## Unit tests

All unit tests (frontend or backend) are located close to the source code in the same folder. For example, a file located at `src/service/` with the name `RandomService.ts` will have a unit test file located at `src/service/RandomService.test.ts`.

Whether it's frontend or backend, you can run unit tests directly inside VSCode with Jest extension for VSCode or you can run in command line with `npm run test`.

:warning: By default, ModernMERN there is no tests for React basic rending when there is no complex logic.

### Next.js page tests

:warning: The behavior for Next.js pages is different. The unit tests are located at `src/pages.test/` instead of the same folder. This avoids Next.js to consider the test as a page.

## Integration tests

The backend also includes integration tests for testing all backend layers: routers, validators, middlewares, controllers and service including the database. They are located at `test/integration/`. For each integration tests, we inject the Express.js app into the `supertest` library. With `supertest`, you can make test at HTTP level: you can simulate POST, GET, DELETE, PUT, etc. requests.

Like the unit tests, you can use VSCode Jest extension to run the test or run `npm run test` command.

## E2E testing

> :warning: Before running E2E tests, in the backend, you need to set `reloadHandler` to `false` in `serverless.yml` file. Otherwise, the backend will throw an `Out of memory` error. Then, you can start the backend with `npm run dev`.

ModernMERN uses Cypress for E2E testing. And, the E2E tests are located in frontend `./cypress` folder. To run the E2E tests, you can run the following command in the frontend project:

```sh
npm run e2e:headless
```

It'll run all the tests in headless mode and you can only see the final results. If you are writing a new test or editing an existing test, you can run the following command in the frontend:

```sh
npm run e2e
```

It'll open the Cypress app where you can easily debug, visual see the results, time travel, and interact with the application.

## Information about the database

For each unit tests or integration tests, it automatically spin up a clean and fresh Database instance. It won't have any side effects between tests.

## Frontend test utils

When a component use the `useSWR` hook, it needs to be wrap around `<SWRConfig>`. You also need to be careful with the React `useAuth` hook, you need to provide a mock authentication to render the component in unit tests. It can be done using `<TestingAuthProvider>` component.

To make it easier to tests with these hooks, you can find in the `src/utils` folder a file called `TestUtils.tsx`. You'll find inside the file several custom renderers. They can be used to render components that use `useSWR` or `useAuth` hook for testing purposes.

## Better testing experience

There are two tools you can use to have better experience to write your frontend tests:

- [Jest Preview](https://github.com/nvh95/jest-preview), you can visually preview your component when working with Jest and React testing library
- [React Testing Library Playground](https://testing-library.com/docs/queries/about/#screenlogtestingplaygroundurl), it'll find the best queries to select elements in your component
- [Testing Playground Extension](https://testing-library.com/docs/queries/about/#browser-extension), React Testing Library Playground in browser extension

## Useful links

- https://kentcdodds.com/blog/static-vs-unit-vs-integration-vs-e2e-tests
- https://kentcdodds.com/blog/common-mistakes-with-react-testing-library
- https://github.com/goldbergyoni/javascript-testing-best-practices
