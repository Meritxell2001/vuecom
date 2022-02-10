<template>
    <input v-model="subcomentario" placeholder="Deja tu comentario" @keypress.enter="guardarMensaje">
    
    <button @click="cargarComentarios">Cargar ya!</button>
    
    <p v-for="comentario in comentarios" :key="comentario.id">
        {{ comentario.texto }}
    </p>
</template>

<script>
    export default {
        name: "app",
        data() {
            return {
                subcomentario: "holaaa",
                comentarios: [
                    { id: 1, texto: "adeu, molt bones" },
                    { id: 2, texto: "holiwiii" },
                    { id: 3, texto: "byeeee" },
                    { id: 4, texto: "holaaas" }
                ]
            }
        },
        methods: {
            guardarMensaje() {
                this.comentarios.push({id: 5, texto: this.subcomentario})
                //guardar en la base de datos
            },
            async cargarComentarios() {
                //Descarreguem les dades de la bbdd
                let respuesta = await fetch("/api/get");
                //Pasem les dades a json
                let respuestaJSON = await respuesta.json();
                //enviem a la variable comentarios les dades aconseguides
                this.comentarios = respuestaJSON;

                //podem fer els 3 pasos en 1 d'aquesta manera:
                //this.comentarios = await (await fetch("/api/get")).json();
            }
        }
    }
</script>

<style scoped>
    input {
        color:cornflowerblue;
        font-family: noteworthy;
    }
</style>