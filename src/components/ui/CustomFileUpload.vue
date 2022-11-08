<template>
    <div class="generic-input">
        <label class="generic-input__label text-sm secondary-color" v-if="label">
            {{ label }}
        </label>

        <!-- INSERIRE PREPEND STILIZZARE -->
        <div class="input-container">
            <slot name="prepend"></slot>
            <input
                type="file"                
                class="generic-input__input-file--hidden"
                ref="inputFileRef"
                @change="handleInputChange"
            >
            <div class="generic-input__input-file">
                <div class="generic-input__input-file__button" @click="handleButtonClick">
                    Sfoglia...
                </div>

                <div class="generic-input__input-file__file">                    
                    <div v-if="!currentFile" class="generic-input__input-file__file__placeholder">
                        {{ placeholder }}
                    </div>
                    
                    <div v-else class="generic-input__input-file__file__file-name">
                        {{ currentFile.name }}

                        <div class="generic-input__input-file__file__file-name__cancel">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="#FFFFFF" class="cancel">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                            </svg>
                        </div>                        
                    </div>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue";

export default defineComponent({
    name: 'CustomFileUpload',
    props: {
        label: {
            type: String as PropType<string>,
            required: false
        },
        placeholder: {
            type: String as PropType<string>,
            required: false,
            default: 'Nessun file selezionato'
        }       
    },
    setup() {
        const inputFileRef = ref(null);

        const handleButtonClick = () => {
            inputFileRef.value.click();
        }

        const currentFile = ref<File>(null);
        const handleInputChange = ({ target }) => {
            if(target && target.files.length > 0) {
                currentFile.value = target.files[0];
            }
        }        

        return {
            inputFileRef,
            handleButtonClick,
            handleInputChange,
            currentFile,
        }
    }
})
</script>

<style scoped lang="scss">
.generic-input {
    &__input-file {
        &--hidden {
            display: none;
        }

        display: flex;
        width: 100%; 
        font-size: 16px;         
        box-shadow: none;
        border-radius: 5px;
        font-family: 'Montserrat';
        color: $secondary_color;   

        &__button {
            padding: 10px 12px;
            border: 1px solid lighten($color: $secondary_color, $amount: 40);
            border-top-left-radius: 5px;
            border-bottom-left-radius: 5px;
            font-weight: 500;
            cursor: pointer;
        }

        &__file {
            padding: 10px 12px;
            flex-grow: 1;
            border: 1px solid lighten($color: $secondary_color, $amount: 40);
            border-top-right-radius: 5px;
            border-bottom-right-radius: 5px;
            border-left-width: 0;

            &__placeholder {
                color: lighten($color: $secondary_color, $amount: 20)
            }

            &__file-name {
                font-weight: 500;   
                position: relative;      
                
                &__cancel {
                    position: absolute;
                    right: 0;
                    top: 0;
                    height: 25px;
                    width: 25px;
                    border-radius: 50%;
                    background-color: red;
                    display: flex;
                    align-items: center;
                    justify-content: center;   
                    // transform: translateY(-50%);  
                    cursor: pointer;               
                }
            }
        }
    }
}
</style>