<template>
	<svg xmlns="http://www.w3.org/2000/svg" :width="width" :height="height" :viewBox="`0 0 ${canevas.width} ${canevas.height}`" fill="currentColor" class="w-6 h-6">
		<defs>
			<marker id="Start" overflow="visible" markerHeight="3" markerWidth="1" orient="auto" preserveAspectRatio="xMidYMid" viewBox="0 0 1 8">
				<path id="fleche" d="m-1.5-12v24h3v-9.9785l10.355 5.9785v-16l-10.355 5.9785v-9.9785z" fill="#fff" />
			</marker>
			<marker id="Stop" overflow="visible" markerHeight="3" markerWidth="1" orient="auto" preserveAspectRatio="xMidYMid" viewBox="0 0 1 8">
				<use href="#fleche" transform="scale(-1 1)" />
			</marker>
			<filter id="papier" x="0" y="0" width="1" height="1" color-interpolation-filters="sRGB">
				<feTurbulence baseFrequency="0.01" numOctaves="2" result="papier1" type="fractalNoise" />
				<feDisplacementMap in="SourceGraphic" in2="papier1" result="papier2" scale="0" xChannelSelector="R" yChannelSelector="G" />
				<feDiffuseLighting lighting-color="#FFF" in="papier1" result="papier3" surfaceScale="2">
					<feDistantLight azimuth="235" elevation="40" />
				</feDiffuseLighting>
				<feComposite in="papier2" in2="papier3" operator="in" />
				<feComposite in2="papier3" k1="1.7" operator="arithmetic" result="papier4" />
				<feBlend in="papier4" in2="papier2" />
			</filter>
			<filter id="trait" x="-.03" y="-.03" width="1.06" height="1.06" color-interpolation-filters="sRGB">
				<feTurbulence baseFrequency="0.5" type="fractalNoise" />
				<feColorMatrix result="trait1" values="0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 1 1 1 2 -1.5" />
				<feGaussianBlur in="SourceGraphic" result="trait2" stdDeviation=".3" />
				<feComposite in="trait2" in2="trait1" operator="in" />
			</filter>
		</defs>
		<rect class="papier" width="100%" height="100%" />
		<g class="traits">
			<rect class="frame" :x="frame.x" :y="frame.y" :width="frame.width" :height="frame.height" fill="#fff" />
			<rect class="plank" :x="frame.x" :y="(i - 1) * (plank.height + plank.gap) + frame.y" v-for="i in plank.n" :width="plank.width" :height="plank.height" />
		</g>
		<g class="dimensions" stroke-width="2" stroke="#FFF" marker-start="url(#Start)" marker-end="url(#Stop)">
			<dimension-component :debut="{x: frame.x, y:frame.y - margin / 2}" :fin="{x: frame.x + frame.width, y:frame.y - margin / 2}">{{ dimensions.length }} feet</dimension-component>
			<dimension-component :debut="{x: frame.x - margin / 2, y: (frame.height + canevas.height) / 2}" :fin="{x: frame.x - margin / 2, y: (canevas.height - frame.height) / 2}">{{ dimensions.depth }}feet</dimension-component>
		</g>
	</svg>
</template>

<script setup>
import DimensionComponent from './Dimension.vue';
import { ref, computed } from 'vue';
const margin = 50;
const props = defineProps({
	height: {
		type: Number,
		default: 500,
	},
	width: {
		type: Number,
		default: 500,
	},
	dimensions: {
		type: Object,
		default: () => ({
			length: 0,
			depth: 0,
		}),
	},
	canevas: {
		type: Object,
		default: () => ({
			width: 600,
			height: 500,
		}),
	},
	plank: {
		type: Object,
		default: {
			orientation: 'length',
			length: 8,
			depth: 5.5 / 12,
			gap: 1 / 8 / 12,
		},
	},
});
const ratio = computed(() => {
	return props.dimensions.length / props.dimensions.depth <= props.canevas.width / props.canevas.height
		? (props.canevas.height - margin * 2) / props.dimensions.depth
		: (props.canevas.width - margin * 2) / props.dimensions.length;
	// return (1000 - margin * 2) / Math.max(props.dimensions.length, props.dimensions.depth);
});
console.log(ratio.value);
const frame = computed(() => {
	const width = props.dimensions.length * ratio.value;
	const height = props.dimensions.depth * ratio.value;
	const x = (props.canevas.width - width) / 2;
	const y = (props.canevas.height - height) / 2;
	return {
		x,
		y,
		width,
		height,
	};
});
const plank = computed(() => {
	const width = frame.value.width;
	const height = props.plank.depth * ratio.value;
	const x = (1000 - width) / 2;
	const y = (1000 - height) / 2;
	const n = Math.floor(props.dimensions.depth / props.plank.depth);
	const gap = props.plank.gap * ratio.value;
	return {
		x,
		y,
		width,
		height,
		n,
		gap,
	};
});
</script>

<style lang="scss">
.frame {
	fill: transparent;
	stroke: #f00;
	stroke-width: 6;
	stroke-dasharray: 2, 12;
	stroke-linecap: round;
}

.traits {
	filter: url(#trait);
}
.dimension {
	filter: url(#trait);
}
.papier {
	filter: url(#papier);
	fill: hsl(216, 74%, 20%);
}

.plank {
	fill: transparent;
	stroke: #fff;
	stroke-width: 2;
}
</style>