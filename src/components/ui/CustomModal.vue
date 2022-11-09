<template>
    <div class="custom-modal" v-if="isOpen">
        <div class="modal-background">
            <div class="modal-container">
                <div class="modal-header">
                    <div class="modal-title">
                        <template v-if="!withoutTitle">{{ modalTitle }}</template>
                    </div>
                    <div class="modal-close" @click="emitCloseModal">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" width="24px" height="24px">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </div>
                </div>

                <div class="modal-body">
                    <slot name="modal-body"></slot>
                </div>

                <div class="modal-footer">
                    <slot name="modal-footer"></slot>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
export default defineComponent({
    name: 'CustomModal',
    props: {
        isOpen: {
            type: Boolean as PropType<boolean>,
            required: false,
            default: false
        },
        modalTitle: {
            type: String as PropType<string>,
            required: false,
            default: 'Titolo modale'
        },
        withoutTitle: {
            type: Boolean as PropType<boolean>,
            default: false
        }
    },
    setup(props, context) {

        const emitCloseModal = () => {
            context.emit('closeModal');
        }

        return { emitCloseModal }
    }
});
</script>

<style lang="scss">
.custom-modal {
    width: 100%;
    height: 100vh;
    position: fixed;
    left: 0;
    top: 0;

    .modal-background {
        height: 100%;
        width: 100%;
        background-color: rgba(0, 0, 0, 0.7);
        display: flex;
        align-items: center;
        justify-content: center;

        .modal-container {
            background-color: #fff;
            padding: 22px;
            border-radius: 8px;
            width: 85%;
            max-width: 750px;
            display: flex;
            flex-direction: column;   
            max-height: 80vh;         

            .modal-header {
                display: flex;
                justify-content: space-between;
                align-items: center;
                color: $secondary_color;
                font-weight: 600;
                stroke: $secondary_color; 
                margin-bottom: 15px;
                
                .modal-title {
                    font-size: 18px;
                }
                
                .modal-close {
                    cursor: pointer;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                }
            }

            .modal-body {
                flex-grow: 1;
                overflow: auto;
            }

            .modal-footer {
                margin-top: 10px;
                display: flex;
                justify-content: flex-end;
            }
        }
    }
}
</style>