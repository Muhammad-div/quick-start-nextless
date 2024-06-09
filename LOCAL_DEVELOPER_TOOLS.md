
### Tools for developer experience in local environment

#### VSCode extensions

ModernMERN comes up with Settings for a seamless integration with VSCode. The Debug configuration is also provided for frontend and backend debugging experience. You don't need to do anything special for the Settings and the Debug in VSCode.

But, for extensions, you need to install the suggested extensions from `.vscode/extension.json`. This file is present for each repository.

With the plugins installed on your VSCode, ESLint and Prettier can automatically fix the code and show you the errors. You don't even need to think about code formatting anymore.

Pro tips: if you need a project wide type checking with TypeScript, you can run a build with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>B</kbd> on Mac.

#### Database GUI

For better developer experience with your local database, you can use Prisma Studio:

```shell
npx prisma studio
```

#### Local SES (Amazon Email Service)

ModernMERN comes with a local SES server for testing emails. Under the hood, it uses `serverless-offline-ses-v2` and `aws-ses-v2-local`. It helps you visualize the emails you send from your backend.

When the backend send an email, you can see the result at http://localhost:8005. Exactly like the Serverless functions and DynamoDB, AWS Email Service is also simulated in local environment. So, you can work offline without internet connection.

> :warning: When your browser have a tab opened at http://localhost:8005, you need to close the tab before stopping the backend server.
