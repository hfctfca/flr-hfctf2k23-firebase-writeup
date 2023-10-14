# Flag 6 - Bonus Read the Almanac

1. As Biff, trying to recursively read the App storage ``gs://$project_id.appspot.com/app`` will fail.
1. From the loaded ``gs://$project_id.appspot.com/app/assets/js/main.js`` and the location of the Web site static assets ``/assets`` try to download another Web site asset from the storage (i.e. ``gs://$project_id.appspot.com/app/assets/js/main.js``) and see that it is working.
1. List all the Web Site static assets and retrieve there metadata:
  
    ```js
    firebase.storage.ref("/app/assets/img/favicon-16x16.png");
    ```
