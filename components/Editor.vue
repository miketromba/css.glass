<template>
	<div class="editor gradient-bg-wiretap">
		<style>
        .glass {
            {{ css }}
        }
		</style>

		<Preview />

		<div class="panels">
			<div class="panel glass">
				<div class="editor-setting">
                    <div class="header"><span>TRANSPARENCY</span></div>
                    <Slider @change="updateTransparency" :min="0" :max="MAX_TRANSPARENCY" :interval="INTERVAL_TRANSPARENCY" :initialValue="INITIAL_TRANSPARENCY" ref="transparencySlider" />
                </div>
				<div class="editor-setting">
                    <div class="header"><span>BLUR</span></div>
                    <Slider @change="updateBlur" :min="0" :max="MAX_BLUR" :interval="INTERVAL_BLUR" :initialValue="INITIAL_BLUR" />
                </div>
				<div class="editor-setting">
                    <div class="header"><span>COLOR</span></div>
                    <ColorPicker :rgba="color" @change="updateColor" />
                </div>
				<div class="editor-setting">
                    <div class="header"><span>OUTLINE</span></div>
                    <Slider @change="updateOutlineAlpha" :min="0" :max="MAX_TRANSPARENCY" :interval="INTERVAL_TRANSPARENCY" :initialValue="INITIAL_OUTLINE_ALPHA" />
                </div>
			</div>
			<div class="panel glass">
                <div class="header noselect">CSS</div>
                <pre>{{ css }}</pre>
            </div>
		</div>
	</div>
</template>

<script>
const MAX_TRANSPARENCY = 1
const INTERVAL_TRANSPARENCY = .01
const INITIAL_TRANSPARENCY = .2
const MAX_BLUR = 20
const INTERVAL_BLUR = .1
const INITIAL_BLUR = 5
const INITIAL_COLOR = {
    r: 255, g: 255, b: 255, 
    a: INITIAL_TRANSPARENCY
}
const INITIAL_OUTLINE_ALPHA = .3

export default {
    data(){
        return {
            MAX_TRANSPARENCY,
            INTERVAL_TRANSPARENCY,
            INITIAL_TRANSPARENCY,
            MAX_BLUR,
            INTERVAL_BLUR,
            INITIAL_BLUR,
            INITIAL_OUTLINE_ALPHA,

            color: {...INITIAL_COLOR},
            blur: INITIAL_BLUR,
            outlineAlpha: INITIAL_OUTLINE_ALPHA,
        }
    },
    computed: {
        css(){
            const outlineCSS = this.outlineAlpha ? `\nborder: 1px solid rgba(${this.color.r}, ${this.color.g}, ${this.color.b}, ${this.outlineAlpha});` : ''

            return `/* Generated from https://website.com */\n\nbackground: rgba(${this.color.r}, ${this.color.g}, ${this.color.b}, ${this.color.a});\nborder-radius: 16px;\nbox-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);\nbackdrop-filter: blur(${this.blur}px);\n-webkit-backdrop-filter: blur(${this.blur}px);${outlineCSS}`
        }
    },
    methods: {
        updateTransparency(val){
            this.color.a = val
        },
        updateBlur(val){
            this.blur = val
        },
        updateColor(rgba){
            this.color.r = rgba.r
            this.color.g = rgba.g
            this.color.b = rgba.b
            this.setTransparencySliderVal(rgba.a)
        },
        setTransparencySliderVal(val){
            this.$refs.transparencySlider.setValue(val)
        },
        updateOutlineAlpha(val){
            this.outlineAlpha = val
        },
    }
}
</script>

<style scoped>
pre {
    margin-top: 12px;
    cursor: text;
}
.panels {
    width: 90%;
    max-width: 500px;
    margin: 0 auto;
    margin-top: 48px;
}
.panel {
    margin-bottom: 18px;
	padding: 14px 18px;
	color: white;
	font-size: 16px;
	font-weight: 300;
}
.editor {
	width: 100%;
	height: 100vh;
	position: relative;
}
.gradient-rainbow {
	background: linear-gradient(
			217deg,
			rgba(255, 50, 50, 1),
			rgba(255, 0, 0, 0) 70.71%
		),
		linear-gradient(127deg, rgba(50, 255, 50, 1), rgba(0, 255, 0, 0) 70.71%),
		linear-gradient(336deg, rgba(50, 50, 255, 1), rgba(0, 0, 255, 0) 70.71%);
}
.gradient-bg-wiretap {
	background: #8a2387; /* fallback for old browsers */
	background: -webkit-linear-gradient(
		320deg,
		#f27121,
		#e94057,
		#8a2387
	); /* Chrome 10-25, Safari 5.1-6 */
	background: linear-gradient(
		320deg,
		#f27121,
		#e94057,
		#8a2387
	); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
</style>
