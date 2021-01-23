<template>
<div class="scattered-previews">
    <div class="glass" v-for="i in POPULATION" :key="i" :style="randomCSS()"></div>
</div>
</template>

<script>
const POPULATION = 20
const MIN = 50
const MAX = 200
const MAX_OPACITY = 0.5

export default {
    data(){
        return {
            POPULATION
        }
    },
    methods: {
        randomCSS(){
            const width = random(MIN, MAX),
                height = random(MIN, MAX),
                top = random(0, window.innerHeight-height+80),
                left = random(0, window.innerWidth-width),
                rotation = Math.random(),
                opacity = ((width * height) / (MAX * MAX)) * MAX_OPACITY

            return `width: ${width}px; height: ${height}px; top: ${top}px; left: ${left}px; transform: rotate(${rotation}turn); opacity: ${opacity};`
        }
    }
}

// https://stackoverflow.com/questions/4959975/generate-random-number-between-two-numbers-in-javascript
function random(min, max){
    return Math.floor(Math.random() * (max - min + 1) + min)
}
</script>

<style scoped>
.scattered-previews {
    position: absolute;
    width: 100%;
    height: 100vh;
    overflow: hidden;
}
.glass {
    position: absolute;
}
</style>