<template>
	<select :name="name" :id="name">
		<option value="in">in</option>
		<option value="ft">ft</option>
		<option value="cm">cm</option>
		<option value="m">m</option>
	</select>
</template>
<script setup>
import { defineProps } from 'vue';
const props = defineProps({
	name: String,
});
</script>