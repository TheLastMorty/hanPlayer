<template>
    <div>
        <audio controls id="audio" ></audio>
    </div>
</template>

<script setup lang="ts">
    import {ref,onMounted } from "vue";

    let src=ref("http://47.113.204.82/music/mecury.mp3")

    onMounted(()=>{
        let audio = document.getElementById('audio');
        // audio.crossOrigin = 'anonymous';
        audio.src=src.value;
        let audioObject = new Audio(src.value)
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        const ctx = new AudioContext();
        const analyser = ctx.createAnalyser();
        analyser.fftSize = 256;
        const source = ctx.createMediaElementSource(audio);
        // source.connect(analyser);
        // var bufferLength = analyser.frequencyBinCount;
        // var dataArray = new Uint8Array(bufferLength);
        // analyser.connect(ctx.destination);
        // analyser.getByteFrequencyData(dataArray)
        // console.log('data :>> ', dataArray);

        audio?.addEventListener("play",(event)=>{
            console.log("play");
            
            
        })
        audio?.addEventListener("ended",(event)=>{
            console.log("end");
        })
        audio?.addEventListener("pause",(evnet)=>{
            console.log("pause");
        })
    })
    

</script>