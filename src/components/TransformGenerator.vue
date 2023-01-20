<template>
	<section class="generator">
		<div class="generator__container">
			<div class="copied" v-if="copied" :class="{copy: copied}">Copied!</div>
			<div class="generator__table">
				<input type="text" v-model="textInput">

				<label class="generator__label">Text color: {{ textColor }}</label>
				<input type="color" v-model="textColor">

				<label class="generator__label">Background: {{ bgColor }}</label>
				<input type="color" v-model="bgColor">

				<label class="generator__label">Rotate: {{ rotate }}deg;</label>
				<input type="range" min="-180" max="180" v-model="rotate">

				<label class="generator__label">Scale: {{ scale }};</label>
				<input type="range" min="0.1" max="2" step="0.1" v-model="scale">

				<label class="generator__label">Translate X: {{ translateX }}px;</label>
				<input type="range" min="-100" max="100" v-model="translateX">

				<label class="generator__label">Translate Y: {{ translateY }}px;</label>
				<input type="range" min="-100" max="100" v-model="translateY">

				<label class="generator__label">Skew X: {{ skewX }}deg;</label>
				<input type="range" min="-90" max="90" v-model="skewX">

				<label class="generator__label">Skew Y: {{ skewY }}deg;</label>
				<input type="range" min="-90" max="90" v-model="skewY">

				<div class="generator__buttons">
					<button class="btn btn-main" @click.prevent="reset">Reset</button>
					<button class="btn btn-success" @click.prevent="copy">Copy</button>
				</div>
			</div>
			<div class="generator__result">
				<div class="generator__border">
					<div class="generator__output" :style="output">
					{{ textInput }}
				</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
export default {
	data() {
		return {
			textColor: '#ffffff',
			bgColor: '#3344c1',
			rotate: 0,
			scale: 1,
			translateX: 0,
			translateY: 0,
			skewX: 0,
			skewY: 0,
			textInput: 'Your text!',
			copied: false,
		}
	},
	computed: {
		output() {
			return {
				transform: `rotate(${this.rotate}deg) scale(${this.scale}) translateX(${this.translateX}px) translateY(${this.translateY}px) skewX(${this.skewX}deg) skewY(${this.skewY}deg)`,
				color: `${this.textColor}`,
				backgroundColor: `${this.bgColor}`
			}
		}
	},
	methods: {
		reset() {
			this.textColor = '#ffffff',
			this.bgColor = '#3344c1',
			this.rotate = 0,
			this.scale = 1,
			this.translateX = 0,
			this.translateY = 0,
			this.skewX = 0,
			this.skewY = 0,
			this.textInput = 'Your text!'
		},
		async copy() {
			let copyText = `
			<div class="box">${this.textInput}</div>

				<style>
					.box {
						padding: 16px 30px;
						transform:${this.output.transform};
						color:${this.output.color};
						background-color:${this.output.backgroundColor};
					}
				</style>
			`
			await navigator.clipboard.writeText(copyText)
			this.copied = true
			setTimeout(() => {
				this.copied = false
			}, 1500)
		}
	}
}
</script>

<style>
input[type="text"] {
	font-family: Montserrat;
	margin-bottom: .5rem;
	font-size: 1rem;
	padding: 5px 8px 4px;
	border: none;
	border-radius: 6px;
	box-shadow: 0 0 0 1px var(--bg-main-color);
}
input[type="text"]:focus {
	outline: none;
	box-shadow: 0 0 0 2px var(--blue-color-hover);
}
input[type="color"] {
	height: 34px;
	border-radius: 6px;
}

.generator__label + input {
	margin-bottom: .5rem;
}
.generator {
	padding: 2.5rem 15px;
}
.generator__container {
	position: relative;
	max-width: 800px;
	margin: 0 auto;
	padding: 15px;
	border-radius: 6px;
	background: var(--bg-second-color);
	display: flex;
	flex-flow: column-reverse;
	row-gap: 15px;
}

.copied {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	padding: 2rem;
	border-radius: 6px;
	background: var(--blue-color-hover);
	z-index: 20;
	text-transform: uppercase;
	font-weight: 600;
}
.copy {
	animation: 1.5s copyAnim linear;
}
@keyframes copyAnim {
	50% {
		opacity: 1;
	}
	100% {
		opacity: 0;
	}
}
.generator__table {
	flex: 1 0 45%;
	color: var(--black-color);
}

.generator__result {
	position: relative;
	flex: 1 0 45%;
	overflow: hidden;
	border-radius: 6px;
	background: var(--white-color);
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 250px;
}

.generator__border {
	padding: 0.5rem;
	border: 1px solid #3344c1;
	border-radius: 6px;
}
.generator__output {
	padding: 0.8rem 1.5rem;
	font-weight: 600;
	border-radius: 6px;
}

.generator__buttons {
	margin: 20px 0 0;
	display: flex;
	gap: 15px;
	justify-content: flex-end;
}

@media screen and (min-width: 768px) {
	.generator__container {
		flex-flow: row;
		column-gap: 15px;
	}
}
</style>