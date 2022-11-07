<template>
    <div class="custom-multiselect">        
        <label 
            for="exampleFormControlSelect1"
            v-if="label"
            class="custom-multiselect__label text-sm"
        >
            {{ label }}
        </label>

        <vue-multiselect 
            v-model="value" 
            :options="options"
            class="custom-multiselect__select"
            :placeholder="placeholder"
            :multiple="true"
            :close-on-select="false"
            selectLabel="Seleziona"
            selectedLabel="Selezionato"
            deselectLabel="Rimuovi"
            track-by="label"
            @search-change="find"
        >     
            <template v-slot:noResult>
                Nessun risultato.
            </template>   

            <template v-slot:tag="props">                                
                <div class="multiselect__tags-wrap">
                    <span class="multiselect__tag">
                        <span>
                            {{ props.option.label }}
                        </span>
                        <i @click="removeOption(props.option)" tabindex="1" class="multiselect__tag-icon"></i>
                    </span>
                </div>
            </template> 

            <template v-slot:option="props">
                {{ props.option.label }}
            </template>
        </vue-multiselect>        
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import VueMultiselect from 'vue-multiselect';
import SelectOptions from '../../types/SelectOptions';

export default defineComponent({
    name: 'CustomMultiSelect',
    props: {
        label: {
            type: String as PropType<string>
        },
        placeholder: {
            type: String as PropType<string>,
            default: 'Seleziona opzione'
        }
    },
    components: {
        VueMultiselect
    },
    data () {
        return {
            value: null,
            options: [
                {
                    label: 'Opzione 1',
                    value: 1
                },
                {
                    label: 'Opzione 2',
                    value: 2
                },
                {
                    label: 'Opzione 3',
                    value: 3
                },
            ]
        }
    },
    methods: {
        removeOption(option) {
            const optionIndex : number = this.value.findIndex((_option : SelectOptions) => {
                return _option.label === option.label && _option.value === option.value; 
            }) 
            const duplicatedOptions = this.value;
            duplicatedOptions.splice(optionIndex, 1);
            this.value = duplicatedOptions;
        },
        find(e) {
            console.log(e);
        }
    }
});
</script>

<style src="vue-multiselect/dist/vue-multiselect.css"></style>
<style lang="scss">
.custom-multiselect {
    display: flex;
    flex-direction: column;    

    &__label {
        color: $secondary_color;
        margin-bottom: 10px;
        text-transform: uppercase;
        font-weight: 700;
    }

    &__select {        
        color: $secondary_color;      

        .multiselect__placeholder {
            font-size: 16px;
            color: $secondary_color;
        }
        
        .multiselect__tags {
            padding-left: 12px;
            border-color: lighten($color: $secondary_color, $amount: 40);

            .multiselect__tag {
                background-color: $primary_color;
                
                i.multiselect__tag-icon:after {
                    color: #fff
                }
            }
        }

        .multiselect__element {
            .multiselect__option--selected.multiselect__option::after {
                color: $primary_color;
            }

            .multiselect__option--highlight.multiselect__option--selected.multiselect__option::after {
                color: #ffffff;
            }                       
        }
    }
}
</style>