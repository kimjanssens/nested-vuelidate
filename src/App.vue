<template>
	<main>
		<pre>{{ formData }}</pre>

		<div>
			<form novalidate @submit.prevent="handleSubmit">
				<div :class="{ error: v$.firstName.$errors.length }">
					<input v-model="formData.firstName" type="text" />

					<small v-for="error of v$.firstName.$errors" :key="error.$uid">
						{{ error.$message }}
					</small>
				</div>

				<button type="submit">Submit</button>
			</form>
		</div>
	</main>
</template>

<script setup>
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

const formData = reactive({});

const formRules = {
	firstName: { required },
};

const v$ = useVuelidate(formRules, formData);

const handleSubmit = async () => {
	const isFormCorrect = await v$.value.$validate();

	if (!isFormCorrect) return;

	console.log("Form submitted");
};
</script>
