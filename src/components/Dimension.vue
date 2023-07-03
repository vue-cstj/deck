<template>
	<g class="dimension">
		<path :d="`M ${points}`" fill="none" />
		<text :transform="`rotate(${angle} ${milieu.x} ${milieu.y})`" :x="milieu.x" :y="milieu.y">
			<tspan><slot>{{ etiquette }}</slot></tspan>
		</text>
		
	</g>
</template>
<script setup>
import { computed, getCurrentInstance } from 'vue';
const {slots} = getCurrentInstance();
const props = defineProps({
	debut: {
		type: Object,
		default: {
			x: 0,
			y: 0,
		},
	},
	fin: {
		type: Object,
		default: {
			x: 100,
			y: 100,
		},
	},
	etiquette: {
		type: String,
		default: '41ft',
	},
});
const milieu = computed(
	() => ({
		x: (props.debut.x + props.fin.x) / 2,
		y: (props.debut.y + props.fin.y) / 2,
	})
);
const angle = computed(() => {
	return Math.atan2(props.fin.y - props.debut.y, props.fin.x - props.debut.x) * (180 / Math.PI);
});
const points = computed(() => {
	const length = Math.sqrt(Math.pow(props.fin.x - props.debut.x, 2) + Math.pow(props.fin.y - props.debut.y, 2));
	const ratioGap =  (length - gap.value) / 2/ length;
	const delta = {
		x: (props.fin.x - props.debut.x) * ratioGap,
		y: (props.fin.y - props.debut.y) * ratioGap,
	};
	return [
		Pt.from(props.debut),
		Pt.sum(props.debut, delta),
		"M"+Pt.diff(props.fin, delta),
		Pt.from(props.fin),
	].join(' ');
});
const gap = computed(() => {
	return (slots.default()[0].children.length + 1) * 13;
});
class Pt {
	constructor(x, y) {
		this.x = x;
		this.y = y;
	}
	toString() {
		return `${this.x} ${this.y}`;
	}
	static from(obj) {
		return new this(obj.x, obj.y);
	}
	static sum(a, b) {
		return new this(a.x + b.x, a.y + b.y);
	}
	static diff(a, b) {
		return new this(a.x - b.x, a.y - b.y);
	}
}
</script>
<style lang="scss">
.dimension {
	text {
		text-rendering: geometricPrecision;
		font-size: 16pt;
		text-anchor: middle;
		dominant-baseline: middle;
		fill: #ffffff;
		font-family: Lucida Console;
		stroke: none;
	}
}
</style>