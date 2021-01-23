<template>
<div class="gradient-bg-wiretap">
    <header>
        <div class="title">css.glass</div>
        <div class="subtitle">by <a href="https://twitter.com/miketromba" target="_blank">@miketromba</a></div>
    </header>
    <div class="pad-top"></div>
    <Editor />
</div>
</template>

<script>
export default {
    head(){
        const title = `Glassmorphism CSS Effect Generator - Glass CSS`
        const desc = `Copy and paste this Glassmorphism CSS snippet into your frontend project for an amazing CSS glass effect.`
        const image = 'https://css.glass/glassmorphism.png'
        return {
            title: title,
            meta: [
                // hid is used as unique identifier. Do not use `vmid` for it as it will not work
                { hid: 'description', name: 'description', content: desc },
                { property: 'og:title', content: title },
                { property: 'og:description', content: desc },
                { property: 'og:image', content: image, },
                { name: 'twitter:title', content: title },
                { name: 'twitter:description', content: desc },
                { name: 'twitter:image', content: image, },
            ]
        }
	},
}
</script>

<style scoped>
header {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    padding: 16px 24px;
}
.title {
    font-size: 28px;
}
.subtitle {
    font-size: 14px;
    margin-top: 4px;
}
a {
    color: rgb(38, 230, 255);
}
@media (max-width: 1300px) {
    .pad-top { padding-top: 80px; }
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