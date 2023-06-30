<template>
	<svg xmlns="http://www.w3.org/2000/svg" :width="width" :height="height" viewBox="0 0 1000 1000" fill="currentColor" class="w-6 h-6">
		<rect width="100%" height="100%" fill="#24467a" />
		<rect class="frame" :x="frame.x" :y="frame.y" :width="frame.width" :height="frame.height" fill="#fff" />
		<rect class="plank" :x="frame.x" :y="(i-1)*(plank.height + plank.gap)+ frame.y" v-for="i in plank.n" :width="plank.width" :height="plank.height" />
	</svg>
</template>

<script setup>
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
// const ratio = (1000 - margin * 2) / Math.max(props.dimensions.length, props.dimensions.depth);
const ratio = computed(() => {
	return (1000 - margin * 2) / Math.max(props.dimensions.length, props.dimensions.depth);
});
console.log(ratio.value);
const frame = computed(() => {
	const width = props.dimensions.length * ratio.value;
	const height = props.dimensions.depth * ratio.value;
	const x = (1000 - width) / 2;
	const y = (1000 - height) / 2;
	return {
		x,
		y,
		width,
		height,
	};
});
console.log(frame.value);
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
console.log(plank.value);
</script>

<style lang="scss">
.frame {
	fill: transparent;
	stroke: #fff6;
	stroke-width: 6;
	stroke-dasharray:2,12;
	stroke-linecap: round;
}
.plank {
	fill: transparent;
	stroke: #fff;
	stroke-width: 1;
}
</style>