<template>
	<main>
		<pre>{{ formData }}</pre>

		<div>
			<form novalidate @submit.prevent="handleSubmit">
				<Person
					v-for="(person, i) in formData.people"
					:key="i"
					:person="person"
				/>

				<button type="submit">Submit</button>
			</form>
		</div>
	</main>
</template>

<script setup>
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

import Person from "@/components/Person.vue";

const formData = reactive({
	people: [{ firstName: "", lastName: "" }],
});

const formRules = {
	people: { required },
};

const v$ = useVuelidate(formRules, formData);

const handleSubmit = async () => {
	const isFormCorrect = await v$.value.$validate();

	if (!isFormCorrect) return;

	console.log("Form submitted");
};
</script>
