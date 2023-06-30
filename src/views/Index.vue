<template>
	<main>
		<section>
			<h1>Les dimensions</h1>
			<form action="">
				<div>
					<label for="length">Unité</label>
					<unit-select name="length-unit" />
				</div>
				<div>
					<label for="length">Longueur</label>
					<input type="number" name="length" id="length" v-model="length" />
				</div>
				<div>
					<label for="depth">Profondeur</label>
					<input type="number" name="depth" id="depth" v-model="depth" />
					<!-- <unit-select name="depth-unit" style="grid-column:3" /> -->
				</div>
				<div>
					<label for="area">Superficie</label>
					<output name="area" id="area" :value="area" />
				</div>
				<!-- <div><button>Calculer</button></div> -->
			</form>
		</section>
		<plan-svg :dimensions="dimensions" />
	</main>
</template>
<script setup>
import { ref, computed } from 'vue';
import UnitSelect from '@/components/UnitSelect.vue';
import PlanSvg from '@/components/Plan.vue';
const length = ref(10);
const depth = ref(8);
const area = computed(() => length.value * depth.value);
const dimensions = computed(() => ({
	length: length.value,
	depth: depth.value,
}));
</script>
<style lang="scss">
main {
	display: grid;
	grid-template-columns: auto auto;
	gap: 1em;
	justify-content: center;
}
form {
	display: grid;
	grid-template-columns: auto 7em;
	justify-content: start;
	gap: .5em;
	align-items: center;
	border: 1px solid #fff8;
	padding: 1em;
	border-radius: .5em;

	label {
		text-align: right;
		grid-column: 1;
	}

	> div {
		display: contents;
	}

	button,
	select {
		color: #fff;
		padding: .5em;
		border: none;
		border-radius: .25em;
		background-color: hsl(var(--hue), var(--sat), 20%);
		// grid-column: 1 / -1;
		font: inherit;
	}

	input,
	output {
		background-color: hsl(var(--hue), var(--sat), 20%);
		border: 0px solid #fff8;
		border-radius: .25em;
		padding: .5em;
		font: inherit;
	}

	input[type=number] {
		-moz-appearance: textfield;
		appearance: textfield;
		margin: 0;
	}

label {
  -webkit-appearance: menulist-button;
  -moz-appearance: menulist-button;
  appearance: checkbox;

}
	input[type=number]::-webkit-inner-spin-button,
	input[type=number]::-webkit-outer-spin-button {
		-webkit-appearance: none;
		margin: 0;
	}

}</style>