# Start customization

### Add upstream remote (only need to set up for the first time)

As you know, ModernMERN continuously receives updates with new features and improvements. In order to always enjoy the latest version of ModernMERN, you need to follow these steps:

- after cloning the the repository to your local machine and creating a new repository on your GitHub account
- in your local machine, you need to run the following command in each Git repository (frontend, backend and infrastructure):

```sh
git remote add upstream git@github.com:Nextlessjs/modernmern-frontend.git # for the frontend
git remote add upstream git@github.com:Nextlessjs/modernmern-backend.git # for the backend
git remote add upstream git@github.com:Nextlessjs/modernmern-infra.git # for the infrastructure
```

### How to update ModernMERN (read this section when you want to update)

You can now update the repositories directly from your local machine by running `git pull upstream main` in each repository (Infra, Backend and Frontend).

Then, you just need to resolve the conflicts and commit/push your changes to your own repository.

> warning: If you have too much merge conflicts, it might be easier to manually copy the changes from the upstream repository to your local repository.

Only if you are working on another machine, you need to add again the remote repository using `git remote add upstream XXXXXXXXXXXXX` (replace `XXXXXXXXXXXXX` by the correct value) and run the `git pull upstream main`.
