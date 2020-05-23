# A Personalized TodoApp using ReactJS and Firebase
A TodoApp using ReactJS and Firebase

# Requirements

We will use the following components in this application:

- ReactJS
- Material UI
- Firebase
- ExpressJS
- Postman


# Application Architecture
[](https://www.freecodecamp.org/news/content/images/2020/04/TodoApp-1.png)

# Section 1: Developing Todo APIs
In this section, we are going to develop these elements:

- Configure the firebase functions.
- Install the Express framework and build Todo APIs.
- Configuring firestore as database.

Install the firebase tools in your machine use the command below:

```npm install -g firebase-tools```

Then you will receive the following message.

```
+ firebase-tools@8.4.0
added 31 packages from 78 contributors and updated 11 packages in 129.321s
```

Then You need to choose the account to connect Firebase CLI Login. Type ```firebase login``` and follow the process.
After that, you will see the message : Firebase CLI Login Successful


Once that is done then use the command 'firebase init' to configure the firebase functions in your local environment. Select the following options when initialising the firebase function in the local environment:

1. Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choices => Functions: Configure and deploy Cloud Functions
2. First, let’s associate this project directory with a Firebase project …. => Use an existing project
3. Select a default Firebase project for this directory => application_name
4. What language would you like to use to write Cloud Functions? => JavaScript
5. Do you want to use ESLint to catch probable bugs and enforce style? => N
6. Do you want to install dependencies with npm now? (Y/n) => Y

```Shell
C:\Users\firebase-todo> firebase init

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  C:\Users\firebase-todo

? Are you ready to proceed? Yes
? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confir
m your choices. Functions: Configure and deploy Cloud Functions

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

? Please select an option: Use an existing project
? Select a default Firebase project for this directory: todoapp (TodoApp)
i  Using project todoapp (TodoApp)

=== Functions Setup

A functions directory will be created in your project with a Node.js
package pre-configured. Functions can be deployed with firebase deploy.

? What language would you like to use to write Cloud Functions? JavaScript
? Do you want to use ESLint to catch probable bugs and enforce style? No
+  Wrote functions/package.json
+  Wrote functions/index.js
+  Wrote functions/.gitignore
? Do you want to install dependencies with npm now? Yes
```


```
✔ Firebase initialization complete!
```

# Reference
