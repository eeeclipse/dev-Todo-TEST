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

Now open the index.js under functions directory and copy-paste the following code:
```
const functions = require('firebase-functions');

exports.helloWorld = functions.https.onRequest((request, response) => {
     response.send("Hello from Firebase!");
});
```


Deploy the code to firebase functions using the following command:

```
firebase deploy
```

Once the deployment is done you will get the following logline at the end of your command line:

```
> ✔  Deploy complete!
> Project Console: https://console.firebase.google.com/project/todoapp
```

Go to the Project Console > Functions and there you will find the URL of the API. The URL will look like this:
```
https://<hosting-region>-todoapp-<id>.cloudfunctions.net/helloWorld
```

Copy this URL and paste it in the browser. You will get the following response:

```
Hello from Firebase!
```

This confirms that our Firebase function has been configured properly.


## Install the Express Framework:
Now let’s install the Express framework in our project using the following command:

```npm i express```

Now let's create an APIs directory inside the functions directory. Inside that directory, we will create a file named todos.js. Remove everything from the index.js and then copy-paste the following code:

```
//index.js

const functions = require('firebase-functions');
const app = require('express')();

const {
    getAllTodos
} = require('./APIs/todos')

app.get('/todos', getAllTodos);
exports.api = functions.https.onRequest(app);
```

We have assigned the getAllTodos function to the /todos route. So all the API calls on this route will execute via the getAllTodos function. Now go to the todos.js file under APIs directory and here we will write the getAllTodos function.

```
//todos.js

exports.getAllTodos = (request, response) => {
    todos = [
        {
            'id': '1',
            'title': 'greeting',
            'body': 'Hello world from sharvin shah' 
        },
        {
            'id': '2',
            'title': 'greeting2',
            'body': 'Hello2 world2 from sharvin shah' 
        }
    ]
    return response.json(todos);
}
```


Here we have declared a sample JSON object. Later we will derive that from the Firestore. But for the time being we will return this. Now deploy this to your firebase function using the command firebase deploy. It will ask for permission to delete the module helloworld – just enter y.

## Firebase Firestore
We will use a firebase firestore as a real-time database for our application. Now go to the Console > Database in Firebase Console. 


Ignore the DocumentID key. For the field, type, and value, refer to the JSON down below. Update the value accordingly:

```
{
    Field: title,
    Type: String,
    Value: Hello World
},
{
    Field: body,
    Type: String,
    Value: Hello folks I hope you are staying home...
},
{
    Field: createtAt,
    type: timestamp,
    value: Add the current date and time here
}
```


Press the save button. You will see that the collection and the document is created. Go back to the local environment. We need to install `firebase-admin` which has the firestore package that we need. Use this command to install it:

```
$ npm i firebase-admin
+ firebase-admin@8.12.1
```

Create a directory named util under the functions directory. Go to this directory and create a file name admin.js. In this file we will import the firebase admin package and initialize the firestore database object. We will export this so that other modules can use it.

```
//admin.js

const admin = require('firebase-admin');

admin.initializeApp();

const db = admin.firestore();

module.exports = { admin, db };
```

Now let’s write an API to fetch this data. Go to the todos.js under the functions > APIs directory. Remove the old code and copy-paste the code below:
```
//todos.js

const { db } = require('../util/admin');

exports.getAllTodos = (request, response) => {
	db
		.collection('todos')
		.orderBy('createdAt', 'desc')
		.get()
		.then((data) => {
			let todos = [];
			data.forEach((doc) => {
				todos.push({
                    todoId: doc.id,
                    title: doc.data().title,
					body: doc.data().body,
					createdAt: doc.data().createdAt,
				});
			});
			return response.json(todos);
		})
		.catch((err) => {
			console.error(err);
			return response.status(500).json({ error: err.code});
		});
};
```

Here we are fetching all the todos from the database and forwarding them to the client in a list.

You can also run the application locally using `firebase serve` command instead of deploying it every time. When you run that command you may get an error regarding credentials. 





# Reference
