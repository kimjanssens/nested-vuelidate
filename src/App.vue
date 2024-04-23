<template>
	<main class="container mx-auto">
		<div class="grid grid-cols-3 gap-8">
			<pre>{{ formData }}</pre>

			<div class="col-span-2 bg-gray-100 p-8 rounded-lg">
				<form novalidate @submit.prevent="handleSubmit">
					<Person
						v-for="(person, i) in formData.people"
						:key="i"
						:person="person"
						@delete="formData.people.splice(i, 1)"
					/>

					<button type="button" class="px-4 py-2">Add person</button>

					<button
						type="submit"
						class="bg-gray-600 hover:bg-gray-800 text-white px-4 py-2 mt-4 transition-colors ease-in-out duration-300 rounded-md"
					>
						Submit
					</button>
				</form>
			</div>
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
