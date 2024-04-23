<template>
	<main>
		<pre>{{ form }}</pre>

		<div>
			<form novalidate @submit.prevent="handleSubmit">
				<input v-model="form.name" type="text" />

				<button type="submit">Submit</button>
			</form>
		</div>
	</main>
</template>

<script setup>
import { reactive } from "vue";

const form = reactive({});

const handleSubmit = () => {
	console.log("Form submitted");
};
</script>
