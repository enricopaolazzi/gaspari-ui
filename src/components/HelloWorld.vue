<template>
	<div class="tor">
		<h1>{{ name }}</h1>

		<generic-input
			type="text"
			placeholder="Aggiungi un placeholder"
			label="Lorem ipsum"	
			v-model="name"	
			:read-only="true"
		></generic-input>	

		<generic-input
			type="number"
			placeholder="Aggiungi un placeholder"
			label="Lorem ipsum"	
			max="100"	
		></generic-input>	

		<generic-input
			type="date"
			placeholder="Aggiungi un placeholder"
			label="Lorem ipsum"	
			v-model="name"	
		></generic-input>	

		<custom-text-area
			label="ratataaa"
			placeholder="Aggiungi un placeholdert"
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


		<div style="padding: 8px">			
			<custom-multi-checkbox
				:options="options"
				v-model:value="heroes"				
			/>
		</div>	

		<div style="padding: 8px">			
			<custom-radio-group
				:options="[
					{
						id: 'input_444',
						label: 'Radio 1',
						value: 'radio_1',
						name: 'radio_group',						
						disabled: true
					},
					{
						id: 'input_445',
						label: 'Radio 2',
						value: 'radio_2',
						name: 'radio_group',
					}
				]"
				v-model:value="selectedRadioValue"
			/>

			<div>SelectedRadio: {{ selectedRadioValue }}</div>
		</div>	

		<div style="padding: 8px; margin-bottom: 500px">			
			<custom-select
				name="custom_select"
				label="Seleziona"
				:options="[
					{
						value: 1,
						label: 'Giovanni'
					},
					{
						value: 2,
						label: 'Mario'
					},
					{
						value: 3,
						label: 'Andrea'
					},
				]"
				v-model:value="selectedOption"
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
import CustomRadioGroup from './ui/CustomRadioGroup.vue';
import CustomSelect from './ui/CustomSelect.vue';

export default defineComponent({
	name: 'HelloWorld',	
	components: {
		GenericInput,
		CustomTextArea,
		CustomCheckbox,
		CustomMultiCheckbox,
		CustomRadioGroup,
		CustomSelect
	},
	setup() {
		const name = ref<string>('Gianni');		
		let selectedValues = ref<string[]>(['Angular']);

		const selected = ref<boolean>(true);

		const heroes = ref<string[]>(['Luther','Ben', 'Vanya']);

		const options = ref<MultiCheckboxOptions[]>([
			{ label: "Luther", id: 'Luther' },
			{ label: "Diego", id: 2 },
			{ label: "Allison", id: 3 },
			{ label: "Klaus", id: 4 },
			{ label: "Five", id: 5 },
			{ label: "Ben", id: 'Ben' },
			{ label: "Vanya", id: 'Vanya' },
		]);

		const selectedRadioValue = ref<number | string>('radio_1');

		const selectedOption = ref<number | string>(null);

		const test = (e) => {
			console.log(e)
		}

		return { name, selectedValues, selected, test, heroes, options, selectedRadioValue, selectedOption }
	}
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
