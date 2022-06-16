<script setup>
import axios from "axios";
import ZoomMtgEmbedded from '@zoomus/websdk/embedded'
import { ref } from "vue";
  
  const client = ZoomMtgEmbedded.createClient();
  const sdkKey = import.meta.env.VITE_SDK_KEY;
  const meetingNumber = ref();
  const passWord = ref("");
  const role = ref(0);
  const signatureEndpoint = "http://localhost:4000";
  const userEmail = "";
  const userName = "Vue.js";
  const registrantToken = "";
    
  const getSignature = () => {
    axios.post(signatureEndpoint, {
      meetingNumber: meetingNumber.value,
      role: role.value
    })
    .then(res => {
      console.log(res.data.signature);
      startMeeting(res.data.signature);
    })
    .catch(error => {
      console.log(error);
    });
  };

  const startMeeting = (signature) => {
    let meetingSDKElement = document.getElementById('meetingSDKElement');
    client.init({
      debug: true,
      zoomAppRoot: meetingSDKElement,
      language: 'en-US',
      customize: {
        meetingInfo: ['topic', 'host', 'mn', 'pwd', 'telPwd', 'invite', 'participant', 'dc', 'enctype'],
        toolbar: {
          buttons: [
            {
              text: 'Custom Button',
              className: 'CustomButton',
              onClick: () => {
                console.log('custom button');
              }
            }
          ]
        }
      }
    });
    client.join({
      sdkKey: sdkKey,
      signature: signature,
      meetingNumber: meetingNumber.value,
      password: passWord.value,
      userName: userName,
      userEmail: userEmail,
      tk: registrantToken
    })
  };
</script>

<template>
    <main>
        <h1>Zoom Meeting SDK in Vue.js 3.2</h1>

        <!-- For Component View -->
        <div id="meetingSDKElement">
            <!-- Zoom Meeting SDK Component View Rendered Here -->
        </div>
        <input id="meeting-number" type="number" v-model="meetingNumber" placeholder="meeting ID"/><br>
        <input id="meeting-password" type="password" v-model="passWord" placeholder="meeting password"/><br>
        <button @click="getSignature">Join Meeting</button>
    </main>
</template>

<style scoped>
main {
  width: 70%;
  margin: auto;
  text-align: center;
}
main button {
  margin-top: 20px;
  background-color: #2D8CFF;
  color: #ffffff;
  text-decoration: none;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 40px;
  padding-right: 40px;
  display: inline-block;
  border-radius: 10px;
  cursor: pointer;
  border: none;
  outline: none;
}
main button:hover {
  background-color: #2681F2;
}
input[type="number"]::-webkit-outer-spin-button, 
input[type="number"]::-webkit-inner-spin-button { 
  -webkit-appearance: none; 
  margin: 0; 
} 
</style>
