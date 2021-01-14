<template>
<div>
    <div class="editor-color-picker">
        <div class="hover-bar" @click="onClick">
            <div class="color-preview-bar" :class="{ expanded }" :style="`background: rgba(${this.r}, ${this.g}, ${this.b}, 1);`"></div>
        </div>
    </div>
    <ChromePicker 
        v-if="expanded"
        :value="rgba" 
        v-click-outside="onClickOutside"
        @input="onInput"
    />
</div>
</template>

<script>
import { Chrome } from 'vue-color'

export default {
    props: ['rgba'],
    components: { ChromePicker: Chrome },
    computed: {
        r(){ return this.value? this.value.r : this.rgba.r },
        g(){ return this.value? this.value.g : this.rgba.g },
        b(){ return this.value? this.value.b : this.rgba.b },
        a(){ return this.value? this.value.a : this.rgba.a },
    },
    data(){
        return {
            expanded: false,
            value: null
        }
    },
    methods: {
        onInput(val){
            this.value = val.rgba
            this.$emit('change', val.rgba)
        },
        onClick(){
            this.expanded = !this.expanded
        },
        onClickOutside(e){
            if(
                !e.target.className.includes('color-preview-bar') 
                && !e.target.className.includes('hover-bar')
            ){ this.expanded = false }
        }
    },
    directives: {
        'click-outside': {
            bind: function (el, binding, vnode) {
                el.clickOutsideEvent = function (event) {
                // here I check that click was outside the el and his children
                if (!(el == event.target || el.contains(event.target))) {
                    // and if it did, call method provided in attribute value
                    vnode.context[binding.expression](event);
                }
                };
                document.body.addEventListener('click', el.clickOutsideEvent)
            },
            unbind: function (el) {
                document.body.removeEventListener('click', el.clickOutsideEvent)
            }
        }
    }
}
</script>

<style scoped>
.editor-color-picker {
    position: relative;
}
.color-preview-bar {
    height: 8px;
    width: 100%;
    border-radius: 8px;
    margin: 16px 0;
    transition: height .15s ease;
}
.color-preview-bar.expanded {
    height: 30px;
}
.hover-bar {
    height: 30px;
    width: 100%;
    border-radius: 8px;
    margin: 7px 0;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
}
.hover-bar:hover .color-preview-bar {
    height: 30px;
}
</style>

<style>
.vc-chrome {
    border-radius: 8px !important;
    overflow: hidden;
    border: none !important;
    background: rgba(255,255,255,1) !important;
    position: absolute;
    z-index: 100000;
    top: 16px;
    right: 16px;
}
.vc-chrome-body {
    background: transparent !important;
}
.vc-input__input {
    background: rgba(255,255,255,0.2) !important;
    border-radius: 6px !important;
    color: rgba(0,0,0,0.8) !important;
    border: 1px solid rgba(0,0,0,0.2) !important;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1) !important;
}
.vc-input__label {
    color: rgba(0,0,0,0.8) !important;
    font-family: 'Inter', sans-serif;
    font-weight: 600;
}
.vc-chrome-toggle-icon path {
    fill:  rgba(0,0,0,0.8) !important;
}
.vc-chrome-toggle-icon-highlight {
    background: rgba(255,255,255,0.2) !important;
    border: 1px solid rgba(255,255,255,0.6);
}
.vc-chrome-active-color {
    border: 1px solid rgba(0,0,0,0.2);
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.vc-alpha {
    border-radius: 10px;
    height: 11px !important;
    border: 1px solid rgba(0,0,0,0.2);
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.vc-alpha-checkboard-wrap {
    border-radius: 10px;
}
.vc-hue-container {
    border-radius: 10px;
    height: 11px !important;
    border: 1px solid rgba(0,0,0,0.2);
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.vc-hue {
    border-radius: 10px !important;
}
.vc-chrome-hue-wrap {
    border-radius: 10px;
}
</style>
