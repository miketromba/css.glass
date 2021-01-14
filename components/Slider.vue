<template>
<div class="editor-slider">
    <VueSlider @change="onChange" :min="min" :max="max" :interval="interval" :value="initialValue" ref="slider" />
</div>
</template>

<script>
import VueSlider from 'vue-slider-component'

export default {
    props: ['min', 'max', 'interval', 'initialValue'],
    components: { VueSlider },
    data(){
        return {
            value: this.initialValue
        }
    },
    methods: {
        onChange(val){
            this.$emit('change', val)
        },
        setValue(val){
            this.$refs.slider.setValue(val)
        }
    }
}
</script>

<style scoped>
.editor-slider {
    padding: 12px 0;
}
</style>

<style>
.vue-slider-rail {
    background: rgba(255,255,255,0.6);
    border-radius: 4px;
}
.vue-slider-dot-handle {
    background: rgba(255,255,255,0.4);
    border: 2px solid rgba(255,255,255,0.4);
    width: 22px;
    height: 22px;
    border-radius: 22px;
    margin-top: -4px;
    margin-left: -4px;
    cursor: pointer;
}
.vue-slider-dot-tooltip {
    display: none;
}
</style>