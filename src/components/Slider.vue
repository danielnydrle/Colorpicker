<template>
	<div>
		<input :class="isColor" class="slider has-output-tooltip is-circle" type="range" min="0" max="255" step="1" id="sliderInput" v-model="sliderInput" @change="$emit('sliderChange', [color, sliderInput, sliderHex])">
		<div class="columns has-text-centered">
			<div class="column is-half-tablet">
				<output for="sliderInput">{{sliderInput}}</output>
			</div>
			<div class="column is-half-tablet">
				<output for="sliderInput">#{{sliderHex}}</output>
			</div>
		</div>
	</div>
</template>

<script>
import "../../node_modules/bulma-slider/dist/css/bulma-slider.min.css"

export default {
	name: "Slider",

	data() {
		return {
			sliderInput: 0,
		}
	},
	props: ["color"],
	computed: {
		sliderHex() {
			let _temp = parseInt(this.sliderInput).toString(16)
			return _temp.length == 2 ? _temp : `0${_temp}`
		},
		isColor() {
			return `is-${this.color}`
		}
	},
	mounted() {
		this.sliderInput = 0
	}
}
</script>

<style>
.slider {
	min-width: 100%;
}
</style>