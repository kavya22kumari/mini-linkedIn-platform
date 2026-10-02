# Firebase Authentication Configuration

Firebase Authentication is used by the application to handle account registration and login.

This guide explains how to create the required Firebase configuration and enable email/password authentication.

## ⚠️ Authentication Must Be Enabled

The application will not be able to register or authenticate users until the Email/Password provider has been enabled in the Firebase project.

---

# 🔥 1. Open Firebase Console

Go to the Firebase Console and either:

* Create a new Firebase project, or
* Open an existing project intended for this application.

Do not use another person's Firebase credentials or configuration in your local setup.

---

# 🔐 2. Enable Authentication

Inside the Firebase project:

1. Open **Authentication** from the Firebase dashboard.
2. Select **Get started** if Authentication has not been initialized yet.
3. Open the **Sign-in method** section.
4. Select **Email/Password**.
5. Enable the provider.
6. Save the configuration.

The application currently relies on email/password authentication.

---

# ⚙️ 3. Register the Web Application

From the Firebase project settings:

1. Open the project's settings.
2. Locate the section for your applications.
3. Add a web application if one has not already been registered.
4. Give the application an appropriate name.
5. Complete the registration process.
6. Copy the generated Firebase web configuration.

The configuration will contain values similar to:

```javascript
const firebaseConfig = {
  apiKey: "your-firebase-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "your-sender-id",
  appId: "your-app-id"
};
```

**Do not copy real credentials into this Markdown file or commit them directly into the source code.**

---

# 🔑 4. Add Firebase Values to Environment Variables

Create `.env.local` in the project root and add the values:

```env
NEXT_PUBLIC_FIREBASE_API_KEY=your-firebase-api-key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your-project-id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
NEXT_PUBLIC_FIREBASE_APP_ID=your-app-id
```

If the project uses a measurement ID, it can also be added:

```env
NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your-measurement-id
```

The Firebase initialization code should read these values from the environment rather than containing the actual project configuration directly.

---

# 🧪 5. Test Authentication

After configuring Firebase:

1. Start the backend.
2. Start the Next.js development server.
3. Open:

```text
http://localhost:3000
```

4. Navigate to the registration page.
5. Create a test account using an email address you control.
6. Confirm that registration succeeds.
7. Log out.
8. Sign in using the same account.

---

# ❗ Common Authentication Problems

## Registration Returns an Error

Check:

* Email/Password authentication is enabled.
* The Firebase project configuration is correct.
* The environment variables contain the correct values.
* The development server was restarted after changing `.env.local`.

## Login Does Not Work

Verify:

* The account was successfully created in Firebase Authentication.
* The entered email and password are correct.
* The Firebase project ID is correct.
* No old Firebase configuration remains in the application.

## Configuration Changes Are Not Applied

After modifying `.env.local`, stop and restart the Next.js development server.

Environment variables are normally loaded when the development process starts.

---

# 🔒 Security Notes

Firebase web configuration values should be managed carefully.

In particular:

* Never commit private API credentials.
* Never expose database passwords.
* Never place service-account private keys in the frontend.
* Keep `.env.local` outside Git.
* Use Firebase Authentication rules and project restrictions appropriately.
* Use a separate Firebase project for development if necessary.

A suitable `.gitignore` should include environment files such as:

```text
.env
.env.local
.env.*
!.env.example
```

---

# ✅ Final Verification

Before considering Firebase setup complete, confirm that:

* [ ] A Firebase project exists.
* [ ] A web application is registered.
* [ ] Email/Password authentication is enabled.
* [ ] Firebase values are stored in environment variables.
* [ ] No real credentials are present in the repository.
* [ ] A test account can be registered.
* [ ] A test account can log in.
* [ ] Logout works correctly.

Once these checks pass, Firebase Authentication should be ready for local development.
