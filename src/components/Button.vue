<template>
    <button 
        v-on:click="formToggle"
        v-bind:style="{background: color}" 
        class="btn"
        >
            {{text}}
        </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String
    },
    methods: {
        formToggle() {
            this.$emit('btn-click')
        }
    }
}
</script>