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
        ></vue-multiselect>        
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import VueMultiselect from 'vue-multiselect'

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
        options: ['list', 'of', 'options']
      }
    }
    // setup(props) {
    //     const value = ref<string | integer>(null);

    //     const op
    // }
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
        background-color: #fff;  
        color: $secondary_color;
        
        span.multiselect__placeholder {
            font-size: 16px;
            color: $secondary_color;
        }

        .multiselect__tags {
            padding-left: 10px;
            border-color: lighten($color: $secondary_color, $amount: 40);
        }
    }
}
</style>