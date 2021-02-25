<template>
    <header>
        <h1>{{title}}</h1>
        <Button color="green" text="Agregar" />
    </header>
</template>

<script>
import Button from './Button'
export default {
    name: 'Header',
    props: {
        title:{
            type: String,
            default: 'Hola, soy Batman'
        }
    },
    components: {
        Button
    }
    
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