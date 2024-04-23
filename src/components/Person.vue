<template>
	<div>
		<div :class="{ error: v$.firstName.$errors.length }">
			<input v-model="person.firstName" type="text" />

			<small v-for="error of v$.firstName.$errors" :key="error.$uid">
				{{ error.$message }}
			</small>
		</div>

		<div :class="{ error: v$.lastName.$errors.length }">
			<input v-model="person.lastName" type="text" />

			<small v-for="error of v$.lastName.$errors" :key="error.$uid">
				{{ error.$message }}
			</small>
		</div>
	</div>
</template>

<script setup>
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

const props = defineProps({
	person: {
		type: Object,
		required: true,
	},
});

const formRules = {
	firstName: { required },
	lastName: { required },
};

const v$ = useVuelidate(formRules, props.person);
</script>
