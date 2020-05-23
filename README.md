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

Once that is done then use the command 'firebase init' to configure the firebase functions in your local environment. Select the following options when initialising the firebase function in the local environment:

1. Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choices => Functions: Configure and deploy Cloud Functions
2. First, let’s associate this project directory with a Firebase project …. => Use an existing project
3. Select a default Firebase project for this directory => application_name
4. What language would you like to use to write Cloud Functions? => JavaScript
5. Do you want to use ESLint to catch probable bugs and enforce style? => N
6. Do you want to install dependencies with npm now? (Y/n) => Y


```
✔ Firebase initialization complete!
```

# Reference
