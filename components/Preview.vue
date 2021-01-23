<template>
<div>
    <div style="padding: 7vh 0;">
        <div class="heading noselect">GLASSMORPHISM</div>
    </div>
    <div class="preview-panel-wrap">
        <div class="preview-panel glass">
            <!-- <span class="preview-text">css.glass</span> -->
        </div>
    </div>
</div>
</template>

<style scoped>
/* .preview-text {
    font-size: 48px;
    color: black;
    font-weight: 600;
} */
.heading {
    font-size: 6vw;
    color: white;
    font-weight: 400;
    text-align: center;
    text-shadow: 0 4px 10px rgba(0,0,0,0.2);
}
@media (max-width: 1300px) {
    .heading { font-size: 10vw; }
}
.preview-panel {
    width: 80%;
    max-width: 600px;
    height: 20vh;
    transform: rotate(0.015turn);
    /* display: flex;
    justify-content: center;
    align-items: center; */
}
.preview-panel-wrap {
    display: flex;
    justify-content: center;
    position: absolute;
    top: 3.5vh;
    width: 100%;
}
</style>