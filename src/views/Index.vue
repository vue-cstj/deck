<template>
	<main>
		<h1>Les planches</h1>
		<form action="">
			<div>
				<label for="length">Longueur</label>
				<input type="number" name="length" id="length" v-model="length" />
				<unit-select name="length-unit" style="grid-column:3" />
			</div>
			<div>
				<label for="width">Largeur</label>
				<input type="number" name="width" id="width" v-model="width" />
				<unit-select name="width-unit" style="grid-column:3" />
			</div>
			<div>
				<label for="area">Superficie</label>
				<output name="area" id="area" :value="area" />
			</div>
			<div><button>Calculer</button></div>
		</form>
	</main>
</template>
<script setup>
import { ref, computed } from 'vue';
import UnitSelect from '@/components/UnitSelect.vue';
const length = ref(0);
const width = ref(0);
const area = computed(() => length.value * width.value);
</script>
<style lang="scss">
form {
	display: grid;
	grid-template-columns: auto 10em min-content;
	justify-content: start;
	gap: .5em;
	align-items: center;

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
		grid-column: 1 / -1;
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