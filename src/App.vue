<template>
    <input v-model="sucomentario" placeholder="Deja tu comentario" @keypress.enter="guardarMensaje">
    
    <button @click="cargarComentarios">Cargar ya!</button>
    
    <p v-for="comentario in comentarios" :key="comentario.id">
        {{ comentario.contenido }}
    </p>
</template>

<script>
    export default {
        name: "app",
        data() {
            return {
                sucomentario: "holaaa",
                comentarios: [
                    { id: 1, contenido: "adeu, molt bones" },
                    { id: 2, contenido: "holiwiii" },
                    { id: 3, contenido: "byeeee" },
                    { id: 4, contenido: "holaaas" }
                ]
            }
        },
        methods: {
            guardarMensaje() {
                let resultado = await (await fetch(`/api/add?contenido=${this.sucomentario}`)).json();

                this.comentarios.push({id: resultado.insertID, contenido: this.sucomentario});
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