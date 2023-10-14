# Flag 4 - Biff is weak

1. Noticed that when login with an account the app tries to fecth ``gs://hf2k23-firebase-misc.appspot.com/biffco/flag.json``.
1. Retrieve Biff's email from the reset password email *biff.tannen@biffco.luck*.
1. Acknowledge that the default password policy for ``firebase.auth().currentUser.updatePassword()`` is only 6 characters.
1. Bruteforce the login and log in using ``almanac`` password. (The title of the next flag is a hint)
1. The flag is retrieved upon login while loading ``gs://hf2k23-firebase-misc.appspot.com/biffco/flag.json``.
