<template>
<div>
    <div style="padding: 7vh 0;">
        <h1 class="noselect">GLASSMORPHISM</h1>
    </div>
    <div class="preview-panel-wrap">
        <div class="preview-panel glass"></div>
    </div>
</div>
</template>

<style scoped>
h1 {
    font-size: 6vw;
    color: white;
    font-weight: 400;
    text-align: center;
    text-shadow: 0 4px 10px rgba(0,0,0,0.2);
}
@media (max-width: 1300px) {
    h1 { font-size: 10vw; }
}
.preview-panel {
    width: 80%;
    max-width: 600px;
    height: 20vh;
    transform: rotate(0.015turn);
}
.preview-panel-wrap {
    display: flex;
    justify-content: center;
    position: absolute;
    top: 3.5vh;
    width: 100%;
}
</style>