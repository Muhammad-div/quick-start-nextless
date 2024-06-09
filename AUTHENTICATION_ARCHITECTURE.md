# Authentication in ModernMERN with AWS Cognito

All the authentication is handled by AWS Cognito. So, all data related to authentication is handled by them and they are the source of truth. So, in the database, we don't really store any data related to the authentication.

![Authentication Diagram](images/authentication-strategy.png)

## Backend authentication

ModernMERN uses AWS Cognito to support Email and Social authentication. All important security features is handled by AWS: for example, the application don't store the password or generate the JWT token.

The API gateway is secure by the built-in authorizer AWS IAM from AWS: https://github.com/Nextlessjs/modernmern-backend/blob/main/serverless.yml#L103
All incoming requests need to be authenticated by AWS IAM when we add the authorizer. Only valid requests can trigger the AWS Lambda and call the backend code. For your reference, there isn't any validation happening in our code. We only retrieve the user id which is added by the API gateway: https://github.com/Nextlessjs/modernmern-backend/blob/main/src/handler.ts#L26

After adding the authorizer, we need to grant Cognito users the permission to call the API gateway and pass the authorizer: https://github.com/Nextlessjs/modernmern-backend/blob/main/aws-resources/cognito-policy.yml

## Frontend authentication

In the frontend, we also never work directly with Cognito, we use the Amplify package. It automatically stores the JWT token, refreshes it when needed, does the sign up, does the sign in etc. Amplify is initialized in the Next.js `_app.tsx` file: https://github.com/Nextlessjs/modernmern-frontend/blob/main/src/pages/_app.tsx#L13 and it loads the configuration file at `src/utils/AwsConfig.ts`. And, the file `src/utils/AwsConfig.ts` needs to get values from the environment variables.

Here is some code example using Amplify:

- https://github.com/Nextlessjs/modernmern-frontend/blob/main/src/templates/auth/SignUpForm.tsx#L27
- https://github.com/Nextlessjs/modernmern-frontend/blob/main/src/hooks/UseProviderInfo.ts#L29

To protect page in the frontend, we use a custom React Hook Context provider named `AuthProvider`. The `AuthProvider` will verify if the user is signed in or not. If the user signed in, we call the API backend endpoint `/user/profile` to get user information. Especially, we need to retrieve the team list where he has the right. And, when the user isn't signed in, the user will be redirect to the `login` page where we can sign in with Email or Social solution.

All the user dashboard page need to be protected and only show to signed in user, we use the shared layout feature from Next.js: https://nextjs.org/docs/basic-features/layouts to avoid duplicate code. So, we set the dashboard shell (https://github.com/Nextlessjs/modernmern-frontend/blob/main/src/layout/Shell.tsx) as a layout in all dashboard pages. And, it includes the `AuthProvider`. So, no need to add the `AuthProvider` in every page.
