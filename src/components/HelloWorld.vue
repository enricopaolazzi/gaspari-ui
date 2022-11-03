<template>
	<div class="tor">
		<h1>{{ name }}</h1>

		<generic-input
			type="text"
			@update="handleInputChange"
			placeholder="Aggiungi un placeholder"
			label="Lorem ipsum"	
			disabled		
		></generic-input>	

		<custom-text-area
			label="ratataaa"
			@update="handleInputChange"
			placeholder="Aggiungi un placeholdert"
			modelValue="ggg"
			disabled
		/>

	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import GenericInput from "./ui/GenericInput.vue";
import CustomTextArea from "./ui/CustomTextArea.vue";

export default defineComponent({
	name: 'HelloWorld',	
	components: {
		GenericInput,
		CustomTextArea
	},
	setup() {
		let name = 'Gianni';

		const handleInputChange = (e : string | number) => {
			console.log(e);
		}

		return { name, handleInputChange }
	}
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
