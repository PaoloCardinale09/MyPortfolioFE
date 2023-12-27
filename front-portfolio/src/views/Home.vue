<script >
import axios from "axios";

export default {
    data(){
        return{
            server: "https://localhost:44362",
            projects_end_point: "/api/ProjectsControllerAPI",
            projects: [],
        }
    },
    mounted() {
    // Esegui la richiesta GET all'API
    axios.get(`${this.server}${this.projects_end_point}`)
      .then(response => {
        // Aggiorna l'array di progetti con i dati ricevuti
        this.projects = response.data.$values;
        console.log(this.projects)
      })
      .catch(error => {
        console.error('Errore nella richiesta GET:', error);
      });
  },
};


 

</script>

<template>
    <h1>Home</h1>
    <div>
    <h1>Elenco Progetti</h1>
    <ul>
  <li v-for="project in projects" :key="project.Id">
    {{ project.Name }} - {{ project.Description }}
    <ul>
      <li v-for="image in project.Images.$values" :key="image.Id">
        <img width="200px" :src="`${server}${image.ImageUrl}`" alt="Project Image" />
      </li>
    </ul>
  </li>
</ul>


  </div>
  
</template>

<style scoped>

</style>
