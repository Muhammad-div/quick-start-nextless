# Advanced tips

### Important information (only if you have multiple projects using ModernMERN)

For your information, you don't need to customize the `sst.json` file in ModernMERN Infra for one project. But, when you have multiple projects, it'll have name collision. So, you need to update the name in `sst.json` file by choosing a new name instead `modernmern`. And, don't forget to append the '-infra' at the end of the name.

Same in ModernMERN backend, you don't need to customize the service name in `serverless.yml` file for one project. But, when you have multiple projects, it'll have name collision. So, you need to update the service name in `serverless.yml` file by choosing a new name instead `modernmern`.

The two name in `sst` and `serverless.yml` needs to be the same.

### For better developer experience in local environment

If you want to go further and improve your developer experience, I suggest some [local development tools](LOCAL_DEVELOPER_TOOLS.md) you can install and use.

## How to list all my signed up users?

You see the list of user on your AWS account:

- https://console.aws.amazon.com/cognito/home
- Manage user pools
- Then, select the user pools
- Then after setting the user pools, you can click on 'User and groups'
- You should see all the users.

## Fine-tune Stripe configuration

You can easily configure your Stripe subscription to meet your business requirement.

For example, you can update the settings of the customer portal at this page:

- https://dashboard.stripe.com/settings/billing/portal

where you can find settings for pause, cancellation and downgrading subscription plan. Then, you can find more information in their documentation: https://stripe.com/docs/billing/subscriptions/prorations

You can also configure the payment failure during subscription (not the first payment) on this page:

- https://dashboard.stripe.com/settings/billing/automatic

## Running CRON jobs

You can schedule jobs to be run in the background at defined intervals. For example, you can schedule a job to be run every day at midnight, every week at Sunday midnight, or whatever you want.

First, you need to implement the function you want to schedule. Then, in your `serverless.yml` file in ModernMERN backend, you can add the following line:

```yaml
functions:
  app:
    ...

  foo:
    handler: src/foo.handler
    events:
      - schedule: cron(0 0 * * *)
```

With the previous code, we've created a lambda function named `foo`. The code/logic is located at `src/foo` file and the Node.js function is named `handler`. And, this function will be run every day at midnight.

If you need to go further, you can check out the official documentation: https://www.serverless.com/framework/docs/providers/aws/events/schedule

## Do you suggest any third-party tools to use along ModernMERN?

Tools with free tier:

- Add `Sentry` for error tracking and monitoring. Perfect tool to be notified when something goes wrong in your application.
- Use `Seed.run` for automatic backend and infrastructure deployment integrated to your Git workflow. No need to manually run command line with `Seed.run` anymore. If you choose to use Seed.run, please don't forget to set up your Environment variables: https://seed.run/docs/storing-secrets.html
- Add a better serverless monitoring and debugging tool for production with `Lumigo`. But, there is a lot of alternatives like Dashbird, Epsagon, Tundra.
You can setup an alert in Lumigo. So, you can be notified when something goes wrong by setting up a Programmatic Error: https://docs.lumigo.io/docs/programmatic-errors. For your information, `Lumigo` will increase your AWS cost, it uses some resources that aren't free even if the tool itself has a free tier.

## Why am I limited to send to verified email addresses?

By default, AWS SES is in sandbox mode. And in sandbox mode, you can only send from and to the verified email address. There are also some other restrictions and here are the details: https://docs.aws.amazon.com/ses/latest/dg/request-production-access.html

## How can I replace AWS SES by another email provide?

You can replace AWS SES by the following email provider:

- Sendgrid: https://www.npmjs.com/package/nodemailer-sendgrid
- Postmark: https://www.npmjs.com/package/nodemailer-postmark-transport
- Mandrill: https://www.npmjs.com/package/nodemailer-mandrill-transport
- Mailgun: https://www.npmjs.com/package/nodemailer-mailgun-transport
- Or, you can find other transports compatible with `nodemailer`.

Then, you need update the file `src/services/EmailService.ts` in ModernMERN backend to use the new transport instead of AWS SES.

## How to improve working with complex forms?

ModernMERN uses React Hook Form to handle forms. It's a library that helps you to handle forms in React. For better development experience, there is a developer tools named `@hookform/devtools` you can use to debug forms. You can find more information in their documentation at https://react-hook-form.com/dev-tools/.

There isn't provided by default because it needs to modify the render method.

## How to add a dynamic field/input in your form?

Here is two example explaining how to implement a dynamic input in your form:

- https://codesandbox.io/s/react-hook-form-usefieldarray-nested-arrays-m8w6j?file=/src/index.js
- https://www.youtube.com/watch?v=3YvJg_eNyBc

## Add a copy to clipboard functionality

ModernMERN frontend is already using `react-use` package, a collection of react hooks. You can use it to add a copy to clipboard functionality with the hook provided by `react-use`.

In the past, I've used an alternative NPM library for this functionality: https://www.npmjs.com/package/react-use-clipboard

## How to store files in ModernMERN?

For the storage, I recommend using AWS S3 where you can store files and images. You can easily create a bucket using AWS CDK in ModernMERN Infra. Then, in ModernMERN backend, you can create a new route to upload files to S3 using `presignedUrl`: https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#createPresignedPost-property. Finally, in ModernMERN frontend, you upload the file to this newly created backend route.

## What is the default authentication session duration?

By default, the user is connected for 30 days and it's the default configuration from AWS Cognito. You can change this value and it "Must be between 60 minutes and 3650 days".

## Why choosing TypeScript/JavaScript code for infrastructure instead of Terraform?

Using TypeScript over terraform makes the code consistent. So, you don't need to learn new languages. Frontend, backend and infrastructure all use the same language. Also, TypeScript has a huge ecosystem for developer experience with linter, code formatter, IDE integration, debugging, etc... these configuration are shared between repositories.

## Why no using Next.js API routes?

ModernMERN backend is the equivalent of the Next.js API routes, they are doing the same job. My main concern was try to centralize everything in AWS: -frontend/-backend/-infra all are hosted in AWS. Unfortunately, if the architecture uses API routes, it'll make extremely hard to host on AWS.

## How to uninstall ModernMERN?

To uninstall ModernMERN, you need to delete your frontend application in Amplify Hosting. Then, to uninstall the backend, you need to run `npm run remove-prod` in the backend repository. Finally, you also need to run the same command in your ModernMERN infra repository with the same command `npm run remove-prod`.
