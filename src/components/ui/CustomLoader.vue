<template>
    <div 
        class="spinner-border" 
        :class="size" 
        role="status"
        v-if="loading"
    >
        <span class="sr-only">Loading...</span>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
export default defineComponent({
    name: 'CustomLoader',
    props: {
        loading: {
            type: Boolean as PropType<boolean>,
            default: false
        },
        size: {
            type: String as PropType<string>,
            default: 'default'
        }
    },   
})
</script>

<style lang="scss" scoped>
.spinner-border {
    color: $secondary_color;
    display: inline-block;
    width: 2rem;
    height: 2rem;
    vertical-align: text-bottom;
    border: 0.25em solid $secondary_color;
    border-right-color: transparent;
    border-radius: 50%;
    -webkit-animation: spinner-border .75s linear infinite;
    animation: spinner-border .75s linear infinite;

    &.small {
        height: 25px;
        width: 25px;
        border-width: 3px;
    }

    &.large {
        height: 40px;
        width: 40px;
        border-width: 5px;
    }
}

@keyframes spinner-border {
    100% {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}

.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0,0,0,0);
    white-space: nowrap;
    border: 0;
}
</style>>
