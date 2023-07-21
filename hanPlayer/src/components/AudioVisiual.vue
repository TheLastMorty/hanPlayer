<template>
    <div>
        <ul>
            <li v-for="(item,index) of data" :key="index" @click="changeMusic(item.uri)">{{item.name}}</li>
        </ul>
    </div>
</template>

<script setup lang="ts">

    let context = new AudioContext;
    let audio:Audio;
    let source;
    let analyser;
    let fftsize:number=256;
    let dataArray=new Array(fftsize/2)
    let timeInterval;


    import {reactive } from "vue";
    interface Data{
        name:string;
        uri:string;
    }
    let musicList:Data[]=new Array();
    musicList.push({name:"水星记",uri:"http://47.113.204.82/music/mecury.mp3"})
    musicList.push({name:"凄美地",uri:"http://47.113.204.82/music/qimeidi.mp3"})

    let data=reactive(musicList)

    function changeMusic(musicSrc:string){
        // var context = new AudioContext;
            //加载媒体
        // console.log(musicSrc)
        var audio = new Audio(musicSrc);
        audio.addEventListener("play",(event)=>{
            console.log(musicSrc)
        })
        audio.play()
    }

    function createTimeInterval(){
        return setInterval(()=>{
            analyser.getByteFrequencyData(dataArray);
            console.log(dataArray)
        },1000)
    }

    function clearTimeInterval(){
        if(timeInterval){
            clearInterval(timeInterval)
        }
    }

    function play(){
            var context = new AudioContext;
            //加载媒体
            var audio = new Audio("http://47.113.204.82/music/mecury.mp3");
            // var audio=document.getElementById
            //创建节点
            var source = context.createMediaElementSource(audio);
            var analyser = context.createAnalyser();
            //连接：source → analyser → destination
            source.connect(analyser);
            analyser.connect(context.destination);
            analyser.fftSize = 256;
            var length = analyser.fftSize;
            //创建数据
            // var dataArray = new Uint8Array(length);
            audio.play()
            analyser.getByteFrequencyData(dataArray);
            console.log(dataArray)
            var a=setInterval(() => {
                analyser.getByteFrequencyData(dataArray);
                console.log(dataArray)
            }, 1000);
        }

</script>