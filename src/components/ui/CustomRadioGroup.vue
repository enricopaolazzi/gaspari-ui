<template>

    <div class="custom-radio-group">
        <div
            v-for="option in options"
            :key="option.id"
            :class="{ 'disabled' : option.disabled, 'checked' : option.value == value }"
            class="custom-radio-group__single-radio"
        >            
            <input              
                type="radio" 
                :name="option.name" 
                :id="option.id" 
                :value="option.value"
                :disabled="option.disabled"
                class="custom-radio-group__single-radio__radio-hidden"  
                :checked="option.value == value"   
                @change="checkRadio"
            >
            <span class="custom-radio-group__single-radio__radio"></span>
            <label 
                class="custom-radio-group__single-radio__radio-label" 
                :for="option.id"
            >
                {{ option.label }}
            </label>
        </div>
    </div>
  
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import RadioGroupOptions from '../../types/RadioGroupOptions';

export default defineComponent({
    name: 'CustomRadioGroup',
    props: {
        options: {
            type: Array as PropType<Array<RadioGroupOptions>>
        },
        value: {
            type: [Number, String] as PropType<number | string>
        },        
    },
    setup(props, context) {                           
        const checkRadio = ({ target }) => {
            context.emit('update:value', target.value)
        }  

        return { checkRadio }
    }
});
</script>

<style scoped lang="scss">
.custom-radio-group {  

    &__single-radio {
        $self: &;

        display: flex;
        align-items: center;
        margin-bottom: 15px;
        cursor: pointer;

        &:hover {
            #{ $self }__radio {
                background-color: #f5f6f8;
            }
        }

        &.disabled {
            opacity: 0.6;
            cursor: not-allowed;

            #{ $self }__radio-label {
                cursor: not-allowed;
            }
        }
        
        &__radio-hidden {
            display: none;

            &:checked ~ #{ $self }__radio {
                background-color: $primary_color;     
                border-color: $primary_color;

                &::after {
                    content: '';
                    height: 7px;
                    width: 7px;
                    border-radius: 50%;
                    background-color: #ffffff;
                }
            }       
        }

        &__radio {
            height: 21px;
            width: 21px;
            border-radius: 50%;
            margin-right: 14px;
            border: 1px solid lighten($color: $secondary_color, $amount: 40);
            display: flex;
            align-items: center;
            justify-content: center; 
            transition: all .2s ease-out;                    
        }

        &__radio-label {
            color: $secondary_color;
            cursor: pointer;
        }
    }
}


</style>