<script>
import axios from "axios";
import ZoomMtgEmbedded from '@zoomus/websdk/embedded'
import { ref } from "vue";

export default {
  name: 'HelloWorld',
  created () {
  },
  data () {
    return {
      client: ZoomMtgEmbedded.createClient(),
      // This Sample App has been updated to use SDK App type credentials https://marketplace.zoom.us/docs/guides/build/sdk-app
      sdkKey: import.meta.env.VITE_SDK_KEY,
      meetingNumber: ref(""),
      passWord: ref(""),
      role: 0,
      signatureEndpoint: "http://localhost:4000",
      userEmail: "",
      userName: "Vue.js",
      // pass in the registrant's token if your meeting or webinar requires registration. More info here:
      // Meetings: https://marketplace.zoom.us/docs/sdk/native-sdks/web/component-view/meetings#join-registered
      // Webinars: https://marketplace.zoom.us/docs/sdk/native-sdks/web/component-view/webinars#join-registered
      registrantToken: ''
    }
  },
  methods: {
    getSignature() {
      axios.post(this.signatureEndpoint, {
        meetingNumber: this.meetingNumber,
        role: this.role
      })
      .then(res => {
        console.log(res.data.signature);
        this.startMeeting(res.data.signature);
      })
      .catch(error => {
        console.log(error);
      });
    },
    startMeeting(signature) {
      let meetingSDKElement = document.getElementById('meetingSDKElement');
      this.client.init({
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
      this.client.join({
        sdkKey: this.sdkKey,
        signature: signature,
        meetingNumber: this.meetingNumber,
        password: this.passWord,
        userName: this.userName,
        userEmail: this.userEmail,
        tk: this.registrantToken
      })
    }
  }
}
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
