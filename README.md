# ![BugBusters API Integration Documentation ![BugBusters API Integration Documentation](https://i.ibb.co/RCdFLsf/bugbusters-logo.png)](https://app.swaggerhub.com/apis/BugBusters_HNG/bugbusters/0.0.1) 

## Overview

This document provides an overview of the BugBusters API, outlining its structure, dependencies, setup instructions, and folder organization.

- **Authentication:** Secure user login, registration, and social authentication (Google, Facebook, Twitter), magic link.
  
- **Authorization:** Role-based access control (RBAC) ensures secure access to endpoints (Amin, user roles).
  
- **User Management:** CRUD operations for user profiles, password resets, and profile settings.
  
- **Organization Management:** CRUD operations for managing organizations, with admin-specific routes for organizational settings.
  
- **Email and Messaging:** Endpoints for managing emails, invites, waitlists and messages, including CRUD operations.
  
- **Payment Processing:** Secure endpoints for processing payments.
  
- **Customization:** Configuration options for settings, dashboard, charts, widgets and email templates.
  
- **Error Handling:** Consistent handling of errors with appropriate status codes and messages.


## API Endpoints

All API endpoints can be referenced in the [Bug Busters API_REFERENCE](https://app.swaggerhub.com/apis/BugBusters_HNG/bugbusters/0.0.1) document.

## Database Design

[Database ER diagram](https://dbdiagram.io/d/backend-stage-3-task-6691555b9939893daec97fa6)  

[Database Reference](https://dbdocs.io/cyber330d/BugBusters)  Password == @BugBusters    Public Documentaton for DB

[![Database ER diagram](https://i.ibb.co/whKQSsP/backend-stage-3-task-1.png)](https://dbdiagram.io/d/backend-stage-3-task-6691555b9939893daec97fa6)



## Versioning

This project is versioned to ensure backward compatibility and easy maintenance. The current version is 0.0.1

## Contributors

List of people that helped bring this task to a success

[Contributors list](CONTRIBUTORS.md)

We would like to thank all the members of Team BugBusters for their contributions to Project BugBusters:

- **Judd Ugo (@johndoe)** - Designed organisations and super admin resources and endpoints
- **John Kamau (@John Kamau)** - Designed authentication & user resource and management endpoints
- **Anita Olang (@Anita)** - Designed settings, data exports, widgets, charts, user_data endpoints
- **Timothy Stephen (@dandy-Tim)** - Designed payment, email, invite, waitlist, email template, contact us notifications endpoints and performed design reviews
- **Erasmus E Obeth (@cyber330d)** - Database design and optimisation

Special thanks to everyone who has helped make this project better!

## Folder Structure

```
|--- src
|    |--- controllers
|    |--- database
|    |--- interfaces
|    |--- middlewares
|    |--- routes
|    |--- services
|    |--- utils
|    |--- server.ts
|--- .env
|--- app.ts
|--- .gitignore
|--- package.json
|--- tsconfig.json
|--- swagger.json
```

## Dependencies (Dev)

- Node.js
- TypeScript
- Express
- ts-node-dev
- swagger-jsdoc
- swagger-ui-express
- express

## Getting Started

Before you begin, ensure you have the following installed on your machine:

- [Node.js](https://nodejs.org/) (v14 or later)
- [npm](https://www.npmjs.com/) (Node Package Manager, included with Node.js)
- [Git](https://git-scm.com/)

## Contribution Guide

## Getting Started

#### If you don't have git on your machine, [install it](https://docs.github.com/en/get-started/quickstart/set-up-git).

## Fork this repository

Fork this repository by clicking on the fork button on the top of this page.
This will create a copy of this repository in your account.

## Clone the repository

<img align="right" width="300" src="https://firstcontributions.github.io/assets/Readme/clone.png" alt="clone this repository" />

Now clone the forked repository to your machine. Go to your GitHub account, open the forked repository, click on the code button and then click the _copy to clipboard_ icon.

Open a terminal and run the following git command:

```bash
git clone "url you just copied"
```

where "url you just copied" (without the quotation marks) is the url to this repository (your fork of this project). See the previous steps to obtain the url.

<img align="right" width="300" src="https://firstcontributions.github.io/assets/Readme/copy-to-clipboard.png" alt="copy URL to clipboard" />

For example:

```bash
git clone git@github.com:this-is-you/first-contributions.git
```

where `this-is-you` is your GitHub username. Here you're copying the contents of the first-contributions repository on GitHub to your computer.

## Create a branch

Change to the repository directory on your computer (if you are not already there):

```bash
cd first-contributions
```

Now create a branch using the `git switch` command:

```bash
git switch -c your-new-branch-name
```

For example:

```bash
git switch -c add-alonzo-church
```

### Make Changes

Make your changes to the codebase. Ensure your code follows the project's coding standards and guidelines.

### Run Tests

Run the existing tests to ensure your changes do not break anything. If you added new functionality, write corresponding tests.

```sh
npm run test
```

## commit those changes

Now open `Contributors.md` file in a text editor, add your name to it. Don't add it at the beginning or end of the file. Put it anywhere in between. Now, save the file.

<img align="right" width="450" src="https://firstcontributions.github.io/assets/Readme/git-status.png" alt="git status" />

If you go to the project directory and execute the command `git status`, you'll see there are changes.

Add those changes to the branch you just created using the `git add` command:

## Push changes to GitHub

Push your changes using the command `git push`:

```bash
git push -u origin your-branch-name
```

replacing `your-branch-name` with the name of the branch you created earlier.

<details>
<summary> <strong>If you get any errors while pushing, click here:</strong> </summary>

- ### Authentication Error
     <pre>remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
  remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
  fatal: Authentication failed for 'https://github.com/<your-username>/first-contributions.git/'</pre>
  Go to [GitHub's tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) on generating and configuring an SSH key to your account.

</details>

## Submit your changes for review into Staging

If you go to your repository on GitHub, you'll see a `Compare & pull request` button. Click on that button.

<img style="float: right;" src="https://firstcontributions.github.io/assets/Readme/compare-and-pull.png" alt="create a pull request" />

Now submit the pull request.

<img style="float: right;" src="https://firstcontributions.github.io/assets/Readme/submit-pull-request.png" alt="submit pull request" />

Soon your changes will be merged into the staging branch of this project. You will get a notification email once the changes have been merged.

## Setup Instructions

### 1. Clone the Repository

First, clone the repository to your local machine using Git.

```sh
git clone https://github.com/your-username/[app-name].git
cd [app-name]
```

### 2. Install Dependencies

Navigate to the project directory and install the required dependencies.

```sh
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory of the project and add your environment-specific variables. You can use the provided `.env.example` file as a reference.

```sh
cp .env.example .env
```

Edit the `.env` file to match your environment configuration.

### 4. Compile TypeScript

Compile the TypeScript code to JavaScript.

```sh
npm run build
```

### 5. Run the Development Server

Start the development server with the following command. This will also watch for any changes in your code and automatically restart the server.

```sh
npm run start:dev
```

### 6. Run the Production Server

To run the application in a production environment, use the following command:

```sh
npm run start
```

### 7. Verify the Setup

Open your browser and navigate to `http://localhost:3000/api/v1/` to verify that the application is running correctly.

## Folder Structure

Here's an overview of the project's folder structure:

```
|--- src
|    |--- controllers
          |--- v1
|    |--- database
|    |--- interfaces
|    |--- middlewares
|    |--- routes
|         |--- v1
|    |--- services
|    |--- utils
|    |--- server.ts
|--- .env
|--- app.ts
|--- .gitignore
|--- package.json
|--- tsconfig.json
|---swagger.json
```

## Scripts

Here are some useful npm scripts that you can use during development and production:

- `npm run build`: Compiles the TypeScript code to JavaScript.
- `npm run start:dev`: Starts the development server with live reloading.
- `npm run start`: Starts the production server.
- `npm run test`: Runs the test suite (if available).
- `npm run lint`: Runs the linter to check for code style issues.

## Additional Resources

- [Node.js Documentation](https://nodejs.org/en/docs/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Express Documentation](https://expressjs.com/)
- [swagger Documentation](https://swagger.io/docs/)

By following these steps, you should have your Node.js and TypeScript application up and running. If you encounter any issues, please refer to the documentation of the respective tools or seek help from the community.
## Database Design

[Database ER diagram](https://dbdiagram.io/d/backend-stage-3-task-6691555b9939893daec97fa6)

[Database Reference](https://dbdocs.io/cyber330d/BugBusters)


## API Endpoints

All API endpoints can be referenced in the [Bug Busters API_REFERENCE](https://app.swaggerhub.com/apis/BugBusters_HNG/bugbusters/0.0.1) document.

## Versioning

This project is versioned to ensure backward compatibility and easy maintenance. The current version is 0.0.1
