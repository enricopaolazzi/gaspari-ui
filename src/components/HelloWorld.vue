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
			/>				
		</div>	

		<div>{{selected}}</div>				


		<div style="padding: 8px">			
			<custom-multi-checkbox
				:options="options"
				v-model:value="heroes"				
			/>
		</div>	
	</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import GenericInput from "./ui/GenericInput.vue";
import CustomTextArea from "./ui/CustomTextArea.vue";
import CustomCheckbox from "./ui/CustomCheckbox.vue";
import MultiCheckboxOptions from '../types/MultiCheckboxOptions';
import CustomMultiCheckbox from "./ui/CustomMultiCheckbox.vue";

export default defineComponent({
	name: 'HelloWorld',	
	components: {
		GenericInput,
		CustomTextArea,
		CustomCheckbox,
		CustomMultiCheckbox
	},
	setup() {
		const name = ref<string>('Gianni');		
		let selectedValues = ref<string[]>(['Angular']);

		const selected = ref<boolean>(true);

		const heroes = ref<number[]>([1,3,5]);

		const options = ref<MultiCheckboxOptions[]>([
			{ label: "Luther", id: 1 },
			{ label: "Diego", id: 2 },
			{ label: "Allison", id: 3 },
			{ label: "Klaus", id: 4 },
			{ label: "Five", id: 5 },
			{ label: "Ben", id: 6 },
			{ label: "Vanya", id: 7 },
		]);

		const test = (e) => {
			console.log(e)
		}

		return { name, selectedValues, selected, test, heroes, options }
	}
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
