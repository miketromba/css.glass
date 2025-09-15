<template>
	<div>
		<div style="padding: 7vh 0">
			<div class="heading noselect">GLASSMORPHISM</div>
		</div>
		<div
			class="draggable-glass-wrap"
			:style="dragStyle"
			@pointerdown="onPointerDown"
		>
			<div class="preview-panel glass">
				<!-- <span class="preview-text">css.glass</span> -->
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			dragging: false,
			pointerOffsetX: 0,
			pointerOffsetY: 0,
			posX: 0,
			posY: 0,
			containerLeft: 0,
			containerTop: 0
		}
	},
	computed: {
		dragStyle() {
			return `position: absolute; top: ${this.posY}px; left: ${
				this.posX
			}px; z-index: 2147483647; cursor: ${
				this.dragging ? 'grabbing' : 'grab'
			}; touch-action: none;`
		}
	},
	methods: {
		setInitialPosition() {
			const panelEl = this.$el.querySelector('.preview-panel')
			const editorEl = this.$el.closest('.editor')
			const containerRect = editorEl
				? editorEl.getBoundingClientRect()
				: { left: 0, top: 0, width: window.innerWidth }
			this.containerLeft = containerRect.left
			this.containerTop = containerRect.top
			const panelWidth = panelEl
				? panelEl.getBoundingClientRect().width
				: Math.min(containerRect.width * 0.8, 600)
			const initialX = Math.max((containerRect.width - panelWidth) / 2, 0)
			const baselineY = window.innerHeight * 0.035
			let initialY = baselineY
			if (window.innerWidth <= 600) {
				const headerEl = document.querySelector('header')
				const headerBottom = headerEl
					? headerEl.getBoundingClientRect().bottom
					: 0
				const margin = 12
				initialY = Math.max(
					baselineY,
					headerBottom + margin - this.containerTop
				)
			}
			this.posX = initialX
			this.posY = initialY
		},
		onPointerDown(event) {
			const editorEl = this.$el.closest('.editor')
			const containerRect = editorEl
				? editorEl.getBoundingClientRect()
				: { left: 0, top: 0 }
			this.containerLeft = containerRect.left
			this.containerTop = containerRect.top
			this.dragging = true
			this.pointerOffsetX = event.clientX - this.containerLeft - this.posX
			this.pointerOffsetY = event.clientY - this.containerTop - this.posY
			if (event.target && event.target.setPointerCapture) {
				try {
					event.target.setPointerCapture(event.pointerId)
				} catch (e) {}
			}
			window.addEventListener('pointermove', this.onPointerMove, {
				passive: false
			})
			window.addEventListener('pointerup', this.onPointerUp, {
				passive: true
			})
			event.preventDefault()
		},
		onPointerMove(event) {
			if (!this.dragging) return
			this.posX = event.clientX - this.containerLeft - this.pointerOffsetX
			this.posY = event.clientY - this.containerTop - this.pointerOffsetY
			event.preventDefault()
		},
		onPointerUp() {
			this.dragging = false
			window.removeEventListener('pointermove', this.onPointerMove)
			window.removeEventListener('pointerup', this.onPointerUp)
		}
	},
	mounted() {
		this.setInitialPosition()
		window.addEventListener('resize', this.setInitialPosition)
	},
	beforeDestroy() {
		window.removeEventListener('resize', this.setInitialPosition)
		window.removeEventListener('pointermove', this.onPointerMove)
		window.removeEventListener('pointerup', this.onPointerUp)
	}
}
</script>

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
	text-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}
@media (max-width: 1300px) {
	.heading {
		font-size: 10vw;
	}
}
.preview-panel {
	width: 80vw;
	max-width: 600px;
	height: 20vh;
	transform: rotate(0.015turn);
	/* display: flex;
    justify-content: center;
    align-items: center; */
}
.draggable-glass-wrap {
	display: flex;
	justify-content: center;
	width: auto;
}
</style>
