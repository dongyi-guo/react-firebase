# Redesign your React application to make use of Firebase instead of using the standard Express-MongoDB server

1. In order to configure your application to communicate with the Firebase server, you need to install the Firebase module
- it provides the tool and infrastructure that enables you to communicate with the Firebase server.
```
npm init
npm install --save firebase
```
## for more info: https://www.npmjs.com/package/firebase

2. to reconfigure react application, go to src>firebase folder and modify config.js to include "Your" web app's Firebase configuration

3. next, go to src>firebase folder and modify firebase.js
- this is where we configure our application to communicate with the Firebase Server.
-  import the config here. And then import firebase from firebase
- next, initial the app here by supplying the config to the firebase, so this is where you supply all the configuration information so that your client can communicate with the Firebase Server
- In addition, I am exporting a few of these exports from here called auth, fireauth and so on. These I will make use of in the action creators in order to communicate with my Firebase Server.

## Now after this, the major modifications will be in the ActionCreators file
1. So instead of using the fetch, as we did earlier, we are now going to use firestore
2. So as you can see, I have imported the auth, firestore, fireauth, and firebasestore from the firebase module that I have set up earlier in the firebase folder.
3. In order to fetch a collection from my Firebase, we simply say firestore.collection, and then supply the name of the collection.
(And then you can add to the collection by saying, add--takes the specific item that you're adding into your collection there--So that's the document that we're adding into our collection--So this is for the post comment)
4. when you post that, then you will supplied back with a docRef, which is the reference to the document, which then you can use to go and fetch the document from your server.

5. Now the way Firebase works is that it'll supply the ID separately from the actual contents of the documents. So Firebase keeps the ID and the document data itself separately. 
- the data that is in the document is obtained by saying doc.data
- the id of the document is obtained by doc.id
* for instance, for comments, you have to explicitly combine the two (id and data) together into a JavaScript object here, called comment here.
- within our React code, we have always stored the id and the data together as a single JSON document here, or JavaScript object here. So that's why I'm combining the two together into a single JavaScript 

6. So for the login, the auth that we have imported from the firebase, the auth is the one that allows me to do the login and logout
- So if you are logging in using email and password, it provides with this method called signInWithEmailAndPassword. And then you supply the email and password as the two parameters here. 
- And then that will enable you to login. And when you login, the auth provides this object called the currentUser on the auth.
- So you obtain the user's information by saying auth.currentUser

7. for logging out the user I simply say auth.signOut

## Now again, the documentation of how to make use of the Filebase npm module is all available in the Firebase documentation
# again, for more info: https://www.npmjs.com/package/firebase

* when you need to post items, you would say [add], and when you need to get an item, you will say [get]

* you can even get an item from a specific document in the collections. If you want a specific document in the collection, you will say [.doc()] and then you supply the id of the document here
- for instance, **.doc(docRef.id).get()**

8. Now for the favorites to be stored in my Firebase, the favorites are stored as the user ID and the dish ID here
- Now firestore itself doesn't have any way of populating the dish information into the dish ID. So I'm just fetching all the dish information, so this is every favorite is a pair, user and dish ID pair.
- So I'm just fetching that into my favorites here. But then that also means that I need to modify my favorites component so it can use the dish ID and then index into the dishes that are stored in my Redux store, and obtain the dish information

* Or the alternative would be to go to the server and then fetch the information. But since I already have the data about the dishes in my Redux store, because I have already done the fetch dishes to fetch all the information about the dishes. I'm just directly going into the dishes object in my Redux store and fetch this information.

9. In the main component, you would notice that when I do the favorite here for the dish detail, I would simply have to compare the dish to that dishId. 
- also you will notice that when I call the favorites, in addition to supplying their favorites, I also supply the dishes as one of the props for my favorites. 

10. in the favorite component, you will notice that inside the favorite component down below here, you will notice that, when I am rendering the favorite component. Then, right here in this function here, const favorites, what I am doing is I am going into the favorites dishes, dishes is an array of all the dishIds here, so I map through that
- So look at each dishId, then from the dishes, I filtered out that particular dish. And then obtained the dishId, so here you'll see me using the JavaScript array filter here. It will filter out that specific dish information and then render that particular dish

