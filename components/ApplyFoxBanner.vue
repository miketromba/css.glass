<template>
	<a class="af-link" href="https://applyfox.ai" target="_blank">
		<div class="applyfox-bg">
			<div>
				<span class="af-new">NEW</span>
				<span class="af-text">
					🔥 Auto-Apply to 100's of Jobs With AI 🔥
				</span>
			</div>
			<div class="af-url">
				👉
				<span style="font-weight: 400; font-size: 14px"
					>Click to visit:</span
				>
				<span style="text-decoration: underline">ApplyFox.ai</span>
			</div>
		</div>
	</a>
</template>
<style scoped>
.applyfox-bg {
	background-image: url('/applyfox-bg.png');
	background-position: center; /* Center the image */
	background-repeat: repeat; /* Do not repeat the image */
	background-size: cover; /* Resize the background image to cover the entire container */
	padding: 16px;
	border-radius: 8px;
	box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
	margin-bottom: 24px;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	transition: all 0.1s ease;
	border: 4px solid rgba(255, 255, 255, 0.1);
}
.applyfox-bg:hover {
	transform: scale(1.02);
	border: 4px solid rgb(23, 0, 59);
}
.af-link {
	position: relative;
	font-size: 16px;
	font-weight: bold;
	color: white;
	text-decoration: none;
}
.af-new {
	background: #008325;
	border: 1px solid #2aee62;
	box-shadow: 0 0 10px #00ff48b6;
	color: white;
	font-size: 13px;
	padding: 3px 5px;
	border-radius: 4px;
	margin-right: 8px;
}
.af-text {
	margin-top: 8px;
	font-size: 16px;
	margin-top: 4px;
}
.af-url {
	margin-top: 8px;
}
</style>
