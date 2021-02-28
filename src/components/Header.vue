<template>
    <header>
        <h1>{{title}}</h1>
        <Button 
            v-on:btn-click="$emit('toggle-add-task')" 
            v-bind:color="showAddButton ? 'red' : 'green' " 
            v-bind:text="showAddButton ? 'Cerrar Formulario' : 'Abrir Formulario' "
        />
    </header>
</template>

<script>
import Button from './Button'
export default {
    name: 'Header',
    props: {
        text:{
            type: String
        },
        showAddButton:{
            type: Boolean,
        },
        title:{
            type: String,
            default: 'Hola, soy batman'
        }
    },
    components: {
        Button
    },
    emits: ['toggle-add-task']
    
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>