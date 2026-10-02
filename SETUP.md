# Development Setup Guide

This document explains how to configure the application locally and get the frontend, backend, authentication, and database working together.

## 🚀 1. Configure the Environment

### Frontend

Create a `.env.local` file in the project root:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_FIREBASE_API_KEY=your-firebase-api-key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your-project-id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
NEXT_PUBLIC_FIREBASE_APP_ID=your-app-id
```

### Backend

Create `server/.env`:

```env
MONGODB_URI=mongodb://localhost:27017/mini-linkedin
PORT=5000
```

If Cloudinary is used for media uploads, add its configuration values to the backend environment file as well.

**Keep all environment files private and make sure they are ignored by Git.**

---

# 🔥 2. Firebase Configuration

Firebase is required for user authentication.

### Create the Firebase Project

1. Open the Firebase Console.
2. Create a new Firebase project.
3. Register a web application inside the project.
4. Open the Authentication section.
5. Enable the **Email/Password** sign-in provider.
6. Open the project's application settings.
7. Copy the web-app configuration values.
8. Add them to `.env.local`.

The Firebase configuration should be supplied through environment variables rather than being committed directly to the source code.

For more detailed authentication instructions, see [`FIREBASE_SETUP.md`](./FIREBASE_SETUP.md).

---

# 🍃 3. MongoDB Configuration

The application can use either a local MongoDB installation or MongoDB Atlas.

## Option A — Local MongoDB

1. Install MongoDB.
2. Start the MongoDB service.
3. Use the following connection string:

```text
mongodb://localhost:27017/mini-linkedin
```

4. Place the connection string in `server/.env`:

```env
MONGODB_URI=mongodb://localhost:27017/mini-linkedin
```

## Option B — MongoDB Atlas

1. Create an account on MongoDB Atlas.
2. Create a database cluster.
3. Configure database access.
4. Allow the required network connection.
5. Copy the generated connection string.
6. Add it to `server/.env`.

Example:

```env
MONGODB_URI=your-mongodb-atlas-connection-string
```

Do not commit the actual Atlas connection string if it contains credentials.

---

# ▶️ 4. Start the Development Environment

There are two ways to launch the project.

## Windows Start Script

If the included development script is available, run:

```text
start-dev.bat
```

Alternatively, start the two parts of the application manually.

## Manual Startup

### Terminal 1 — Backend

```bash
cd server
npm run dev
```

### Terminal 2 — Frontend

From the project root:

```bash
npm run dev
```

The frontend and backend should now run independently.

---

# 🌐 5. Open the Application

After both servers have started:

### Frontend

```text
http://localhost:3000
```

### Backend

```text
http://localhost:5000
```

---

# 🛠️ Troubleshooting

## Firebase Authentication Is Not Working

Check the following:

* Firebase Authentication is enabled.
* Email/Password authentication is turned on.
* The Firebase environment variables are correct.
* The Firebase project ID matches the configured project.
* The frontend has been restarted after changing `.env.local`.

## MongoDB Connection Fails

Verify that:

* MongoDB is running if using a local installation.
* The `MONGODB_URI` value is correct.
* The Atlas cluster is available if using MongoDB Atlas.
* Your IP/network is allowed by Atlas.
* Database credentials are valid.

## API Requests Are Failing

Confirm:

* The backend server is running.
* The backend is listening on port `5000`.
* `NEXT_PUBLIC_API_URL` points to the correct backend URL.
* The frontend was restarted after modifying the environment file.

## Port Already in Use

If port `5000` is occupied, change the backend port:

```env
PORT=5001
```

Then update the frontend API URL accordingly:

```env
NEXT_PUBLIC_API_URL=http://localhost:5001/api
```

---

# 📱 6. Verify the Main Features

After the application starts, test the core functionality.

## Create an Account

1. Open the registration page.
2. Enter a test name, email, password, and profile information.
3. Submit the registration form.
4. Confirm that authentication succeeds.
5. Verify that the profile is created.

## Create a Post

1. Open the home/feed page.
2. Enter some text in the post composer.
3. Select **Post**.
4. Confirm that the new post appears in the feed.

## Check the Profile

1. Open the profile page.
2. Confirm that the account information is displayed.
3. Try editing the available profile fields.
4. Check whether the user's posts are displayed.

## Test Login and Logout

1. Log out of the current account.
2. Return to the login page.
3. Sign in again.
4. Confirm that the user's profile and posts remain available.

---

# 🚀 7. Preparing for Deployment

Once the local application has been tested successfully, it can be deployed.

## Frontend

A typical deployment flow is:

1. Push the project to GitHub.
2. Connect the repository to a hosting provider.
3. Configure all required frontend environment variables.
4. Set the production backend API URL.
5. Build and deploy the application.

## Backend

For the Express server:

1. Deploy the `server` directory to a Node.js-compatible hosting service.
2. Add the backend environment variables.
3. Configure the production database connection.
4. Verify the API is accessible.
5. Update the frontend's `NEXT_PUBLIC_API_URL`.

## MongoDB

For production use, MongoDB Atlas can be configured with:

* A dedicated database user
* Appropriate network restrictions
* A production connection string
* Required database permissions

---

# 🔐 Important Before Uploading to GitHub

Before committing the project, verify that the repository does **not** contain:

* `.env`
* `.env.local`
* Database passwords
* MongoDB connection strings containing credentials
* Firebase private configuration
* Cloudinary secrets
* API tokens
* Personal information
* Private deployment configuration

Use environment variables for configuration that should remain outside the repository.
