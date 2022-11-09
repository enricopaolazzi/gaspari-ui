<template>
    <div class="generic-input">
        <label class="generic-input__label text-sm secondary-color" v-if="label">
            {{ label }}
        </label>
        
        <ul class="file-list">
            <li 
                class="file-list-item"
                v-for="(file, index) in fileList"
                :key="index"
            >
                {{ file.name }}

                <div @click="deleteFile(index)" class="item-cancel">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="#FFFFFF" class="cancel">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </div>    
            </li>
        </ul>

        <input
            type="file"
            class="generic-input__input-file--hidden"
            ref="inputFileRef"
            @change="handleInputChange"
        >

        <custom-button
            label="Carica"
            styleType="primary"
            :disabled="false"
            @onClick="handleClick"
        >
            <template v-slot:slot-left>
                <svg style="margin-right: 8px" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="#FFFFFF" width="16px" height="16px">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75V16.5m-13.5-9L12 3m0 0l4.5 4.5M12 3v13.5" />
                </svg>
            </template>
        </custom-button>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue";
import CustomButton from "./CustomButton.vue";

export default defineComponent({
    name: 'CustomMultipleFileUpload',
    components: {
        CustomButton
    },
    props: {
        label: {
            type: String as PropType<string>,
            required: false
        },
        files: {
            type: FormData as PropType<FormData>,
            required: false,

        }
    },
    setup(props, context) {
        const inputFileRef = ref(null);

        const handleClick = () => {
            inputFileRef.value.click();          
        }

        const fileList = ref<Array<File>>([]);
        const handleInputChange = ({ target }) => {
            if(target && target.files.length > 0) {
                fileList.value.push(target.files[0]);         
                
                emitFiles()

                // Svuoto la input
                inputFileRef.value.value = '';
            }
        }

        const deleteFile = (index : number) => {
            if(fileList.value.length > 0) {
                fileList.value.splice(index, 1);

                emitFiles();
            }
        }

        const emitFiles = () => {
            // Prepare form data
            let formData = new FormData();
            fileList.value.forEach(file => {
                formData.append('files', file);
            })
            context.emit('update:files', formData);
        }      

        return {
            handleClick,
            handleInputChange,
            inputFileRef,
            fileList,
            deleteFile,
            emitFiles
        }
    }
});
</script>

<style lang="scss" scoped>
.generic-input {
    &__input-file {
        &--hidden {
            display: none;
        }
    }

    .file-list {
        .file-list-item {
            font-weight: 500;   
            position: relative;   
            padding: 10px 12px;
            padding-right: 40px;  
            border: 1px solid lighten($color: $secondary_color, $amount: 40);
            border-radius: 5px;   
            color: $secondary_color;  
            margin-bottom: 10px;   
            
            &:last-child {
                margin-bottom: 15px;
            }

            .item-cancel {
                position: absolute;
                right: 12px;
                top: 50%;
                height: 25px;
                width: 25px;
                border-radius: 50%;
                background-color: red;
                display: flex;
                align-items: center;
                justify-content: center;   
                transform: translateY(-50%);  
                cursor: pointer;  
                transition: background-color 0.12s ease;

                &:hover {
                    background-color: darken(red, 15%);
                }
                
                .cancel {
                    height: 20px;
                    width: 20px;
                }
            }
        }
    }
}
</style>