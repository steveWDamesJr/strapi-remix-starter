# STRAPI REMIX STARTER: REMIX V2, STRAPI, TYPESCRIPT and TAILWIND.

note: This project was started with love by [Paul](https://github.com/PaulBratslavsky) and design is by [Trecia](https://github.com/TreciaKS).

I love Remix and I am new to Typescript. If you find any bugs or improvements feel free to create an issue. Thank you all for your support and participation.

<-- insert gif of project in action>

## Getting Started

1. Clone the repository locally:

```bash
  git clone https://github.com/PaulBratslavsky/strapi-remix-starter.git
    or
  gh repo clone PaulBratslavsky/strapi-remix-starter
```

2. Run `setup` command to setup frontend and backend dependencies:

```bash
  yarn setup
```

3. Next, navigate to your `/backend` directory and set up your `.env` file. You can use the `.env.example` file as reference:

```bash
HOST=localhost
PORT=1337
APP_KEYS="toBeModified1,toBeModified2"
API_TOKEN_SALT=tobemodified
ADMIN_JWT_SECRET=tobemodified
JWT_SECRET=tobemodified
TRANSFER_TOKEN_SALT=tobemodified
```

4. Start your project by running the following command:

```bash
  yarn build
  yarn develop
```

You will be prompted to create your first admin user.

![admin-user](https://user-images.githubusercontent.com/6153188/231865420-5f03a90f-b893-4057-9634-9632920a7d97.gif)

Great. You now have your project running. Let's add some data.

## Seeding The Data

We are going to use our DEITS feature which will alow to easily import data into your project.

You can learn more about it in our documentation [here](https://docs.strapi.io/dev-docs/data-management).

In the root of our project we have our `seed-data.tar.gz` file. We will use it to seed our data.

1. Open up your terminal and make sure you are still in you `backend` folder.

2. Run the following command to seed your data:

```bash
  yarn strapi import -f ../seed-data.tar.gz
```

![after-import](https://user-images.githubusercontent.com/6153188/231865491-05cb5818-a0d0-49ce-807e-a8 79f7e3070c.gif)

This will import your data locally. Log back into your admin panel to see the newly imported data.

## Setting Up The Frontend

Next we need to switch to our `/frontend` directory and create our `.env` file and paste in the following. 

```bash
  SUBMIT_FORM_STRAPI_KEY=to_be_replaced
  STRAPI_API_URL=http://localhost:1337
  SESSION_SECRET=secret 
```

Before starting our Remix app we need to go inside our Strapi Admin and give public permissions to display our content and create a token that will allow us to submit our **form**

After the import from the `data-seed` file these should be already set.  But we will double check.

Inside your Strapi Admin Panel navigate to Settings -> USERS & PERMISSIONS PLUGIN -> Roles -> Public

In Permissions we should have the following access.

| Content         |   Permissions    |
| --------------- | :--------------: |
| Article         | find and findOne |
| Product-feature | find and findOne |
| Author          | find and findOne |
| Category        | find and findOne |
| Global          |       find       |
| Page            | find and findOne |


Next, let's create a Token to allow us ability to submit our form.

Inside your Strapi Admin Panel navigate to Settings -> API Tokens and click on the `Create new API Token`.

This token will allow us to submit our form.

Name: Public API Form Submit
Description: Form Submission.
Token duration: Unlimited
Token type: Custom

In Permissions lets give the following access.

| Content              | Permissions |
| -------------------- | :---------: |
| Lead-Form-Submission |   create    |

Add your token to your `SUBMIT_FORM_STRAPI_KEY` variable name in the `.env` file.

Once your environment variables are set you can start your frontend application by running `yarn dev`.

You should now see your Remix frontend.

<-- add image -->

## Start Both Projects Concurrently

We can also start both projects with one command using the `concurrently` package.

You can find the setting inside the `package.json` file inside the root folder.

```json
{
  "scripts": {
    "frontend": "yarn dev --prefix ../frontend/",
    "backend": "yarn dev --prefix ../backend/",
    "setup:frontend": "cd frontend && yarn",
    "setup:backend": "cd backend && yarn",
    "setup": "yarn install && yarn setup:frontend && yarn setup:backend",
    "dev": "yarn concurrently \"cd backend && yarn develop\" \"cd frontend && yarn dev\"",
    "repo:upstream": "git fetch upstream && git merge upstream/main"
  },
  "dependencies": {
    "concurrently": "^7.6.0"
  }
}
```

You can start both apps by running `yarn dev`.

## Conclusion

Hope you find this starter useful, it is a bare-bone example to help you get started quickly.

Would love to hear what you will build using it.

If you find bugs or have suggestions feel free to create issues.

Thank you and stay awesome.

# Contributing to the Remix Starter repository

We're so excited that you're thinking about contributing to the Remix Starter open-source project! If you're unsure or afraid of anything, just know that you can't mess up here. Any contribution is valuable, and we appreciate you!

This document aims to provide all the necessary information for you to make a contribution.

## Prerequisites

Before you can contribute, you need to have the following installed:

- Node.js and npm: You can download these from the official [Node.js website](https://nodejs.org/).
- Git: You can find installation instructions for Git in the official [Git Book](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## Steps to Contribute

### 1. Fork the Repository

In your web browser, navigate to [https://github.com/PaulBratslavsky/strapi-remix-starter](https://github.com/PaulBratslavsky/strapi-remix-starter). Click the 'Fork' button in the upper right-hand corner of the page. This creates a copy of the repository in your GitHub account.

### 2. Clone your Fork

Now, go to your version of the repository. You can do this by navigating to https://github.com/USERNAME/strapi-remix-starter (replace 'USERNAME' with your GitHub username). Here, click the 'Clone' button and then 'Copy to clipboard' to copy the git URL.

Next, you need to open your terminal, navigate to where you want to store the project, and type the following command, followed by 'Enter':

```bash
git clone PASTE_CLONED_REPOSITORY_URL
```

Replace 'PASTE_CLONED_REPOSITORY_URL' with the URL you copied earlier. This command downloads your fork to your computer.

### 3. Add Upstream Repository

Before you can start contributing, you have to set up a reference to the original repository. You can do this with the following command:

```bash
git remote add upstream https://github.com/PaulBratslavsky/strapi-remix-starter.git
```

This command adds a new remote, named 'upstream', that points to the original repository.

### 4. Synchronize your Fork

Before you start making changes, you should synchronize your forked repository with the latest changes from the upstream. Here are the steps:

a. Fetch the branches and their respective commits:

```bash
git fetch upstream
```

b. Checkout to the main branch of your fork:

```bash
git checkout main
```

c. Merge changes from the upstream's main branch into your local main branch:

```bash
git merge upstream/main
```

This brings your fork's main branch into sync with the upstream repository, without losing your local changes.

### 5. Create a Branch

When you're making a contribution, it's best to make your changes in a new branch instead of the main branch. You can create a new branch and switch to it using the following command:

```bash
git checkout -b BRANCH_NAME
```

Replace 'BRANCH_NAME' with a name that describes the change you're planning to make.

### 6. Make your Changes

Now, you can start making changes to the project. Feel free to make changes that you think will enhance the project.

### 7. Commit your Changes

When you've made your changes, you need to commit them. This is like creating a save point in a game. You can do this using the following commands:

```bash
git add -A
git commit -m "Your detailed commit message"
```

Replace "Your detailed commit message" with a description of the changes you made.

### 8. Push your Changes

After committing your changes, you need to push them to your forked repository on GitHub. You can do this with the following command:

```bash
git push origin BRANCH_NAME
```

Replace 'BRANCH_NAME' with the name of the branch you created earlier.

### 9. Create a Pull Request

After you've pushed your changes, you're ready to create a pull request (PR). Navigate to your forked repository in your web browser and click on 'Pull request' (near the top of the page), then on 'New pull request'. Ensure that the base fork is the original repository and the base is 'main', and that the head fork is your fork and the compare is the branch you created.

Enter a title for your PR and describe the changes you made. Once you're ready, click 'Create pull request'.

### Congrats! 🎉

You've just made a contribution to the Remix Starter project! The team will review your changes and may suggest some modifications or improvements. Once your changes have been approved, they will be merged into the main codebase.

Thank you for your contribution. We appreciate you!

Remember, everyone was new to open-source at some point. If you're unsure about something, don't hesitate to ask for help. Good luck and happy hacking!

### Psst...

If you find yourself contributing frequently, we've provided a script in the package.json to help keep your local project synchronized with the main branch of the upstream (original) project. Simply execute the following command:

```bash
yarn repo:upstream
```
