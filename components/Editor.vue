<template>
	<div class="editor">
		<span v-html="glassStyleTag"></span>

		<ScatteredPreviewPanels />
		<Preview />

		<div class="panels glass-initial cssPanel" :class="{ wasCopied }">
			<div class="panel">
				<!-- <ApplyFoxBanner /> -->
				<UXCanvasBanner />
				<h1>Glassmorphism CSS Generator</h1>
				<h2>Create a CSS Glass Effect</h2>
				<div class="editor-setting">
					<div class="header noselect"><span>TRANSPARENCY</span></div>
					<Slider
						@change="updateTransparency"
						:min="0"
						:max="MAX_TRANSPARENCY"
						:interval="INTERVAL_TRANSPARENCY"
						:initialValue="INITIAL_TRANSPARENCY"
						ref="transparencySlider"
					/>
				</div>
				<div class="editor-setting">
					<div class="header noselect"><span>BLUR</span></div>
					<Slider
						@change="updateBlur"
						:min="0"
						:max="MAX_BLUR"
						:interval="INTERVAL_BLUR"
						:initialValue="INITIAL_BLUR"
					/>
				</div>
				<div class="editor-setting">
					<div class="header noselect"><span>COLOR</span></div>
					<ColorPicker :rgba="color" @change="updateColor" />
				</div>
				<div class="editor-setting">
					<div class="header noselect"><span>OUTLINE</span></div>
					<Slider
						@change="updateOutlineAlpha"
						:min="0"
						:max="MAX_TRANSPARENCY"
						:interval="INTERVAL_TRANSPARENCY"
						:initialValue="INITIAL_OUTLINE_ALPHA"
					/>
				</div>
				<div class="editor-setting">
					<div class="header noselect">CSS</div>
					<pre>{{ css }}</pre>
					<textarea type="text" v-model="css" ref="input"></textarea>
					<button
						class="copy-button noselect"
						type="button"
						@click="copyCSS"
					>
						Copy CSS to Clipboard
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
const MAX_TRANSPARENCY = 1
const INTERVAL_TRANSPARENCY = 0.01
const INITIAL_TRANSPARENCY = 0.2
const MAX_BLUR = 20
const INTERVAL_BLUR = 0.1
const INITIAL_BLUR = 5
const INITIAL_COLOR = {
	r: 255,
	g: 255,
	b: 255,
	a: INITIAL_TRANSPARENCY
}
const INITIAL_OUTLINE_ALPHA = 0.3

export default {
	data() {
		return {
			MAX_TRANSPARENCY,
			INTERVAL_TRANSPARENCY,
			INITIAL_TRANSPARENCY,
			MAX_BLUR,
			INTERVAL_BLUR,
			INITIAL_BLUR,
			INITIAL_OUTLINE_ALPHA,
			initialCSS: '',

			color: { ...INITIAL_COLOR },
			blur: INITIAL_BLUR,
			outlineAlpha: INITIAL_OUTLINE_ALPHA,

			// Editor state
			wasCopied: false
		}
	},
	computed: {
		css() {
			const outlineCSS = this.outlineAlpha
				? `\nborder: 1px solid rgba(${this.color.r}, ${this.color.g}, ${this.color.b}, ${this.outlineAlpha});`
				: ''
			return `/* From https://css.glass */\nbackground: rgba(${this.color.r}, ${this.color.g}, ${this.color.b}, ${this.color.a});\nborder-radius: 16px;\nbox-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);\nbackdrop-filter: blur(${this.blur}px);\n-webkit-backdrop-filter: blur(${this.blur}px);${outlineCSS}`
		},
		glassStyleTag() {
			return `
            <style>
                .glass-initial {
                    ${this.initialCSS}
                }
                .glass {
                    ${this.css}
                }
            </style>`.trim()
		}
	},
	methods: {
		updateTransparency(val) {
			this.color.a = val
		},
		updateBlur(val) {
			this.blur = val
		},
		updateColor(rgba) {
			this.color.r = rgba.r
			this.color.g = rgba.g
			this.color.b = rgba.b
			this.setTransparencySliderVal(rgba.a)
		},
		setTransparencySliderVal(val) {
			this.$refs.transparencySlider.setValue(val)
		},
		updateOutlineAlpha(val) {
			this.outlineAlpha = val
		},
		copyCSS() {
			copy(this.$refs.input)
			this.wasCopied = true
			setTimeout(() => (this.wasCopied = false), 1500)
		}
	},
	mounted() {
		this.initialCSS = this.css
	}
}

function copy(inputElement) {
	/* Get the text field */
	const copyText = inputElement

	/* Select the text field */
	copyText.select()
	copyText.setSelectionRange(0, 99999) /* For mobile devices */

	/* Copy the text inside the text field */
	document.execCommand('copy')
}
</script>

<style scoped>
h1 {
	font-size: 24px;
	margin-top: 12px;
	text-align: center;
}
h2 {
	font-size: 16px;
	font-weight: 400;
	margin-top: 6px;
	margin-bottom: 24px;
	text-align: center;
}
pre {
	margin-top: 12px;
	cursor: text;
}
.panels {
	width: 90%;
	max-width: 500px;
	margin: 0 auto;
	margin-top: 48px;
	position: relative;
	overflow: hidden;
}
.panel {
	margin-bottom: 18px;
	padding: 14px 18px;
	color: white;
	/* color: #ff306a; */
	font-size: 16px;
	font-weight: 300;
	/* position: relative; */
	overflow: hidden;
}
.editor {
	width: 100%;
	min-height: 100vh;
	position: relative;
	padding-bottom: 24px;
}
.copy-button {
	width: 100%;
	text-align: center;
	padding: 20px;
	background: rgba(255, 255, 255, 0.2);
	border: 2px solid rgba(255, 255, 255, 0.1);
	border-radius: 10px;
	margin-top: 24px;
	cursor: pointer;
	transition: background-color 0.15s ease;
	font-weight: 400;
	font-family: 'Inter', sans-serif;
	text-transform: uppercase;
	/* box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1); */
}
.copy-button:hover {
	background-color: rgba(255, 255, 255, 0.4);
}
textarea {
	position: absolute;
	top: 0;
	bottom: 0;
	opacity: 0.01;
	width: 0px;
	height: 0px;
	pointer-events: none;
}
.cssPanel:after {
	opacity: 0;
	transition: opacity 0.25s ease;
	content: 'Copied to clipboard!';
	display: flex;
	justify-content: center;
	align-items: center;
	position: absolute;
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	color: white;
	font-size: 24px;
	font-weight: 600;
	background: rgba(210, 78, 145, 0.8);
	pointer-events: none;
	z-index: 5;
}
.cssPanel.wasCopied:after {
	opacity: 1;
	pointer-events: all;
}
</style>
