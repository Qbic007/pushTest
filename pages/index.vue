<template>
  <div>
    Push Test
  </div>
</template>

<script>
import { initializeApp } from "firebase/app";
import { getMessaging, getToken } from "firebase/messaging";

const firebaseConfig = {
  apiKey: "AIzaSyAzQEKwbsnd_nj_jRfyv2Qz6q9B9QeUza0",
  authDomain: "ga-push-test.firebaseapp.com",
  projectId: "ga-push-test",
  storageBucket: "ga-push-test.appspot.com",
  messagingSenderId: "482393510768",
  appId: "1:482393510768:web:97b1eec8173390d373b5b5",
  measurementId: "G-Z8R5B8RLFJ"
};

const app = initializeApp(firebaseConfig);

const messaging = getMessaging(app);

const permissionIsGranted = async () => {
  console.log('Requesting permission...');
  await Notification.requestPermission().then((permission) => {
    return permission === 'granted';
  })
}

export default {
  name: 'IndexPage',

  mounted() {
    if (permissionIsGranted) {
      getToken(messaging, {
          vapidKey: 'BEYtlRVxLjrDWhb9jWCRBYmpPyr_X2Z9dJ9aqQ1tqim_OXm91DMoMCDn6cNoRJl6wO5jCMj2eOnpBXRSEyxiyIM'
        }
      ).then((currentToken) => {
        if (currentToken) {
          console.log(currentToken);
        } else {
          console.log('No registration token available. Request permission to generate one.');
        }
      }).catch((err) => {
        console.log('An error occurred while retrieving token. ', err);
      });
    }
  }
}
</script>
