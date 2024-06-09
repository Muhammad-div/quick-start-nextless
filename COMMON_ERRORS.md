# The most common errors and how to fix them

## Infrastructure

### failed: Domain already associated with another user pool

This error occurs when you try to create a new user pool with a domain that is already associated with another user pool. To fix this error, you need to change the environment variable `USER_POOL_DOMAIN` in the `https://github.com/Nextlessjs/modernmern-infra/blob/main/.env.production#L10` file to a different value.

## Backend

### Specified X for function decreases account's UnreservedConcurrentExecution below its minimum value of

The error is caused by the number of concurrent executions of your Lambda functions: https://stackoverflow.com/questions/73988837/aws-specified-concurrentexecutions-for-function-decreases-accounts-unreservedc. To fix this error, you need to decrease the number of concurrent executions of your Lambda functions: https://github.com/Nextlessjs/modernmern-backend/blob/main/serverless.yml#L91. Or, you can even remove this line. By default, the number of concurrent executions is 30 but it's totally arbitrary, so you can set it to any value you want.

### Email address is not verified. The following identities failed the check in region

This error occurs when you try to send an email to an email address that is not verified. To fix this error, you need to verify the email address. AWS SES should send you an email with a link to verify the email address.

## Frontend

### White/Blank user dashboard

This error occurs when you try to access the user dashboard are not able to connect to the backend. Ones of the reasons are:

- The backend is not running
- The backend has an error
- The CORS configuration is not correct

### TypeError: Cannot read properties of undefined (reading 'oauthSignIn')

This error will raised if you didn't set up correctly environment variables in your frontend for AWS Cognito. To fix this error, you need to follow the instructions in https://github.com/Nextlessjs/Modern-MERN-Quick-Start/blob/main/PRODUCTION_DEPLOYMENT.md#deploy-the-frontend and define the environment variables.

### ReferenceError: IntersectionObserver is not defined

This error occurs in testing with Jest. It should happen when you use `Dialog` component and you forget to mock `IntersectionObserver`. To fix this error, you need to add `import '__mocks__/intersectionObserverMock'` to the top of your test file.

### FATAL ERROR: Reached heap limit Allocation failed - JavaScript heap out of memory

This error occurs when you run `npm run check-types`, it usually automatically runs via `lint-staged` when you commit your code. To fix this error, you can upgrade TypeScript to above version 5.1.6.
