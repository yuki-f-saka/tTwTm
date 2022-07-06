<script setup>
import { ref } from 'vue';
import * as sdk from 'microsoft-cognitiveservices-speech-sdk';

let displayText = ref("INITIALIZED: ready to test speech...");

const sttFromMic = () => {
    const speechConfig = sdk.SpeechConfig.fromAuthorizationToken(import.meta.env.VITE_AZURE_AUTHOLIZATION_TOKEN, import.meta.env.VITE_AZURE_REGION);
    speechConfig.speechRecognitionLanguage = 'ja-JP';

    const audioConfig = sdk.AudioConfig.fromDefaultMicrophoneInput();
    const recognizer = new sdk.SpeechRecognizer(speechConfig, audioConfig);

    displayText.value = "speak into your microphone...";

    recognizer.recognizeOnceAsync(result => {

        if(result.reason === sdk.ResultReason.RecognizedSpeech)  {
            displayText.value = `RECOGNIZED: Text=${result.text}`
        } else {
            displayText.value = 'ERROR: Speech was cancelled or could not be recognized. Ensure your microphone is working properly.';
        }
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