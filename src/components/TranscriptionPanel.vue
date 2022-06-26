<script setup>
import { ref } from "vue";

var displayText = ref("INITIALIZED: ready to test speech...");

const sttFromMic = async() => {
    const { speechsdk } = await import('microsoft-cognitiveservices-speech-sdk');
    const speechConfig = speechsdk.SpeechConfig.fromAuthorizationToken("93bce93b4da040629999cde7deebd5ef", "japaneast"); // 必ず.envに記載してそこから取ること！公開するな！
    speechConfig.speechRecognitionLanguage = 'ja-JP';

    const audioConfig = speechsdk.AudioConfig.fromDefaultMicrophoneInput();
    const recognizer = new speechsdk.SpeechRecognizer(speechConfig, audioConfig);

    // this.displayText.value = "speak into your microphone...";

    recognizer.recognizeOnceAsync(result => {

        // if(result.reason === ResultReason.RecognizedSpeech)  {
        //     displayText.value = `RECOGNIZED: Text=${result.text}`
        // } else {
        //     displayText.value = 'ERROR: Speech was cancelled or could not be recognized. Ensure your microphone is working properly.';
        // }
    });
};
</script>

<template>
    <h1 class="display-4 mb-3">Speech sample app</h1>
    <div class="row main-container">
        <div class="col-6">
            <button class="fas fa-microphone fa-lg mr-2" @click="sttFromMic">Convert speech to text from your mic.</button>
        </div>
    </div>
    <div class="col-6 output-display rounded">
        {{displayText}}
    </div>
</template>