<template>
	<div id="app" :style="[isDark ? lightMode : darkMode]">
		<div id="cells">
			<div class="cell" id="c1r1">
				<Slider @sliderChange="update($event)" :color="red"/>
			</div>
			<div class="cell" id="c2r1">
				<Slider @sliderChange="update($event)" :color="green"/>
			</div>
			<div class="cell lastSliderCell" id="c3r1">
				<Slider @sliderChange="update($event)" :color="blue"/>
			</div>
			<div class="cell" id="c1r2">
				<output>{{rgbColor}}</output>
			</div>
			<div class="cell" id="c2r2">
				<div id="rectangle" :style="{'background-color': hexColor}">
				</div>
			</div>
			<div class="cell" id="c3r2">
				<output>{{hexColor}}</output>
			</div>
		</div>
		<button id="switchDarkMode" class="button" :class="{'is-dark': !isDark}" @click="switchDarkMode">
			<span class="icon">
				<i v-if="!isDark" class="far fa-moon"></i>
				<i v-if="isDark" class="far fa-sun"></i>
			</span>
		</button>
	</div>
</template>

<script>
import "../node_modules/@fortawesome/fontawesome-free/css/all.min.css"
import Slider from "./components/Slider.vue"

export default {
	name: 'App',
	components: {
		Slider
	},
	data() {
		return {
			red: "danger",
			green: "success",
			blue: "info",

			lightMode: {
				backgroundColor: "#1a252f",
				color: "#fff"
			},

			darkMode: {
				backgroundColor: "#fff",
				color: "#1a252f"
			},

			isDark: false,

			rgbRed: 0,
			rgbGreen: 0,
			rgbBlue: 0,

			hexRed: "00",
			hexGreen: "00",
			hexBlue: "00",
		}
	},
	methods: {
		update(_event) {
			let _color, _rgb, _hex
			[_color, _rgb, _hex] = _event
			switch (_color) {
				case "danger":
					this.rgbRed = _rgb
					this.hexRed = _hex
					break;
				case "success":
					this.rgbGreen = _rgb
					this.hexGreen = _hex
					break;
				case "info":
					this.rgbBlue = _rgb
					this.hexBlue = _hex
					break;
				default:
					break;
			}
		},
		switchDarkMode() {
			this.isDark = !this.isDark
		},
		reset() {
			this.rgbRed = 0
			this.rgbGreen = 0
			this.rgbBlue = 0
			this.hexRed = "00"
			this.hexGreen = "00"
			this.hexBlue = "00"
		}
	},
	computed: {
		rgbColor() {
			return `(${this.rgbRed}, ${this.rgbGreen}, ${this.rgbBlue})`
		},
		hexColor() {
			return `#${this.hexRed}${this.hexGreen}${this.hexBlue}`
		}
	},
	mounted() {
		this.reset()
	}
}
</script>

<style>
html {
	overflow: hidden;
}
#app {
	width: 100vw;
	height: 100vh;
	font-family: "IBM Plex Mono", monospace;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
}
@media only screen and (min-width: 576px) {
	#cells {
		display: grid;
	}
}
@media only screen and (max-width: 575px) {
	#c3r1 {
		margin-bottom: 10vh;
	}
	#rectangle {
		width: 20vh !important;
		height: 20vh !important;
	}
}
@media only screen and (max-width: 767px) {
	#switchDarkMode {
		position: fixed;
		top: -0.5vw !important;
		right: -0.5vw !important;
	}
}

#switchDarkMode {
	position: fixed;
	top: 2vw;
	right: 2vw;
}

#cells {
	width: 100vw;
	height: 100vh;
	grid-template-columns: 1fr 1fr 1fr;
	grid-template-rows: 1fr 1fr
}
.cell {
	display: flex;
	justify-content: center;
	align-items: center;
}

#c1r1 {
	grid-column: 1;
	grid-row: 1;
}
#c2r1 {
	grid-column: 2;
	grid-row: 1;
}
#c3r1 {
	grid-column: 3;
	grid-row: 1;
}
#c1r2 {
	grid-column: 1;
	grid-row: 2;
}
#c2r2 {
	grid-column: 2;
	grid-row: 2;
}
#c3r2 {
	grid-column: 3;
	grid-row: 2;
}

#rectangle {
	height: 15vw;
	width: 15vw;
}
</style>
