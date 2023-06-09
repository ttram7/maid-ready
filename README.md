# Maid!Ready! Project Repo

- - This version uses React, Redux, Express, Passport, and PostgreSQL (a full list of dependencies can be found in `package.json`).

We **STRONGLY** recommend following these instructions carefully. It's a lot, and will take some time to set up, but your life will be much easier this way in the long run.

# ABOUT MAID!READY!

Maid!Ready! Is a two-sided marketplace app that connects short term rental owners with qualified gig-workers who can clean their properties. It's like "DoorDash" for cleaning services, where owners can post a job with details such as pay rate, address, and a task list that is available to "keepers". Keepers can then log in to Maid!Ready@ and choose jobs based on their preferences, making it easy to find work that fits their lifestyle!

With Maid!Ready Owners can easily access cleaning services without having to search for employees on their own and each Keeper is background checked before being allowed to access the job board. It's the perfect solution for both owners and gig-workers in the short term rental industry.

## Prerequisites

Before you get started, make sure you have the following software installed on your computer:

- [Node.js](https://nodejs.org/en/)
- [PostrgeSQL](https://www.postgresql.org/)
- [Nodemon](https://nodemon.io/)

### Installing ---

## Create the database and tables in SQL

1. - Create a database called `maid_ready_app`.
2. - Create these tables: `user`, `property`, `job`, `checklist_item`, `job_checklist` from the database.sql file.
     ![database.sql-file-location](documentation/images/database-location.png)

**_ If you would like to name your database something else, you will need to change `maid_ready_app` to the name of your new database name in `server/modules/pool.js` file _**

## Development Setup Instructions

- Run `npm install`
- Create a `.env` file at the root directory of this project and paste this line into the file:

  ```
  SERVER_SESSION_SECRET=superDuperSecret
  ```

  \*\*\* While you're in your new `.env` file, take the time to replace `superDuperSecret` with some long random string like `25POUbVtx6RKVNWszd9ERB9Bb6` to keep your application secure.

  - Use this password generator: [https://passwordsgenerator.net/](https://passwordsgenerator.net/).

- .env file creation example: ![env-file-example](documentation/images/env-file-example.png)

  -- replace me section: ![env-file-example](documentation/images/env-file-replace-me.png)

  **_ Fail to complete these steps to create a secret with less than eight characters, OR leave it as `superDuperSecret`, you will get a warning. _**

- Start postgres if not running already by using `brew services start postgresql`
- Run `npm run server`
- Run `npm run client`
- Navigate to `localhost:3000`

## Debugging

To debug, you will need to run the client-side separately from the server. Start the client by running the command `npm run client`. Start the debugging server by selecting the Debug button.

![VSCode Toolbar](documentation/images/vscode-toolbar.png)

Then make sure `Launch Program` is selected from the dropdown, then click the green play arrow.

![VSCode Debug Bar](documentation/images/vscode-debug-bar.png)

## Testing Routes with Postman

To use Postman with this repo, you will need to set up requests in Postman to register a user and login a user at a minimum.

Keep in mind that once you using the login route, Postman will manage your session cookie for you just like a browser, ensuring it is sent with each subsequent request. If you delete the `localhost` cookie in Postman, it will effectively log you out.

1. Start the server - `npm run server`
2. Import the sample routes JSON file [v2](./PostmanPrimeSoloRoutesv2.json) by clicking `Import` in Postman. Select the file.
3. Click `Collections` and `Send` the following three calls in order:
   1. `POST /api/user/register` registers a new user, see body to change username/password
   2. `POST /api/user/login` will login a user, see body to change username/password
   3. `GET /api/user` will get user information, by default it's not very much

After running the login route above, you can try any other route you've created that requires a logged in user!

## Production Build

Before pushing to Heroku, run `npm run build` in terminal. This will create a build folder that contains the code Heroku will be pointed at. You can test this build by typing `npm start`. Keep in mind that `npm start` will let you preview the production build but will **not** auto update.

- Start postgres if not running already by using `brew services start postgresql`
- Run `npm start`
- Navigate to `localhost:5000`

## Lay of the Land

There are a few videos linked below that show a walkthrough the client and sever setup to help acclimatize to the boilerplate. Please take some time to watch the videos in order to get a better understanding of what the boilerplate is like.

- [Initial Set](https://vimeo.com/453297271)
- [Server Walkthrough](https://vimeo.com/453297212)
- [Client Walkthrough](https://vimeo.com/453297124)

Directory Structure:

- `src/` contains the React application
- `public/` contains static assets for the client-side
- `build/` after you build the project, contains the transpiled code from `src/` and `public/` that will be viewed on the production site
- `server/` contains the Express App

This code is also heavily commented. We recommend reading through the comments, getting a lay of the land, and becoming comfortable with how the code works before you start making too many changes. If you're wondering where to start, consider reading through component file comments in the following order:

- src/components

  - AboutPage/AboutPage
  - AddPropertyPagePage/addPropertyPage
  - AdminPage/AdminPage
  - App/App
  - CreateJobForm/CreateJobForm
  - Footer/Footer
  - InfoPage/InfoPage
  - JobDetails/JobDetails
  - JobItem/JobItem
  - LandingPage/LandingPage
  - LoginForm/LoginForm
  - LoginPge/LoginPage
  - LoginSelectionPage/LoginSelectionPage
  - LogOutButton/LogOutButton
  - Nav/Nav
  - OwnerActiveRequest/OwnerActiveRequest
  - OwnerActiveRequestPage/OwnerActiveRequestPage
  - OwnerCompletedRequest/OwnerCompletedRequest
  - OwnerCompletedRequestPage/OwnerCompletedRequestPage
  - OwnerRequestDetails/OwnerRequestDetails
  - OwnerViewRequestsPage/OwnerViewRequestsPage
  - PropertiesPage/PropertiesPage
  - ProtectedRoute/ProtectedRoute
  - RegisterForm/RegisterForm
  - RegisterPage/RegisterPage
  - ProtectedRoute/ProtectedRoute
  - UserPage/KeeperHomePage + OwnersHomePage

## Deployment

1. Create a new Heroku project
1. Link the Heroku project to the project GitHub Repo
1. Create an Heroku Postgres database
1. Connect to the Heroku Postgres database from Postico
1. Create the necessary tables
1. Add an environment variable for `SERVER_SESSION_SECRET` with a nice random string for security
1. In the deploy section, select manual deploy
