<template>
	<label class="wrapper flex items-center">
		{{label}}
		<input 
			class="checkbox" 
			type="checkbox" 
			:checked="isChecked" 
			:value="value" 
			@change="updateInput"
			:disabled="disabled"
		/>
		<span class="checkmark"></span>
	</label>
</template>

<script lang="ts">
import { defineComponent, PropType } from "@vue/runtime-core";

export default defineComponent({
	name: 'CustomSingleCheckbox',
	model: {
		prop: 'modelValue',
		event: 'change'
	},
	props: {
		"value": { type: String },
		"modelValue": { 
			type: Boolean as PropType<boolean>, 			
		},
		disabled: {
			type: Boolean as PropType<boolean>,
			default: false,
		},
		"label": { type: String, required: true},
		"trueValue": { default: true },
		"falseValue": { default: false }
	},	
	computed: {
		isChecked() : boolean {				
			if (this.modelValue instanceof Array) {
				return this.modelValue.includes(this.value)
			}
			// Note that `true-value` and `false-value` are camelCase in the JS
			return this.modelValue === this.trueValue
		}
	},
	methods: {
		updateInput(event) : void {					
			let isChecked = event.target.checked						
			this.$emit('update:checked', isChecked ? this.trueValue : this.falseValue)			
		}
	}
})
</script>

<style lang="scss" scoped>
label.wrapper.flex.items-center {
	color: $secondary_color;
}
.wrapper {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 6px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  font-size: 16px;
}
/* Hide the browser's default checkbox */
.wrapper input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 21px;
  width: 21px;
  border-radius: 2px;
  background-color: #FFFFFF;
  border: 1px solid lighten($color: $secondary_color, $amount: 40);
}

/* On mouse-over*/
.wrapper:hover input ~ .checkmark {
  background-color: #f5f6f8;
}

/* When the checkbox is checked */
.wrapper input:checked ~ .checkmark {
  background-color: $primary_color;
  border-color: var(--primary-color)
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}
/* Show the checkmark when checked */
.wrapper input:checked ~ .checkmark:after {
  display: block;
}
/* Style the checkmark/indicator */
.wrapper .checkmark:after {
  left: 7px;
  top: 3px;
  width: 3.5px;
  height: 7.5px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>