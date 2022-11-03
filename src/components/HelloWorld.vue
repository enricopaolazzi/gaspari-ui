<template>
	<div class="tor">
		<h1>{{ name }}</h1>

		<generic-input
			type="text"
			placeholder="Aggiungi un placeholder"
			label="Lorem ipsum"	
			v-model="name"	
		></generic-input>	

		<custom-text-area
			label="ratataaa"
			placeholder="Aggiungi un placeholdert"
			modelValue="ggg"
			disabled			
		/>

		<div style="padding: 8px">
			<custom-checkbox
				label="porca troiaW"
				value="react"
				v-model:checked="selected"	
				:disabled="true"						
			/>			
		</div>		

		<div>{{selected}}</div>				
	</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import GenericInput from "./ui/GenericInput.vue";
import CustomTextArea from "./ui/CustomTextArea.vue";
import CustomCheckbox from "./ui/CustomCheckbox.vue";

export default defineComponent({
	name: 'HelloWorld',	
	components: {
		GenericInput,
		CustomTextArea,
		CustomCheckbox
	},
	setup() {
		const name = ref<string>('Gianni');		
		let selectedValues = ref<string[]>(['Angular']);

		const selected = ref<boolean>(false);

		const test = (e) => {
			console.log(e)
		}

		return { name, selectedValues, selected, test }
	}
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
