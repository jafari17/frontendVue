<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @star="handelStar" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import axios from "axios";
import SingleProject from "@/components/SingleProject.vue";

export default {
  name: 'HomeView',
  components: {SingleProject},
  data(){
    return {
      projects: [],
    }
  },
  mounted(){
    axios
        .get("http://127.0.0.1:8000/project/")
        .then(response => {
          this.projects = response.data
          console.log(this.projects)
        })
  },
    methods: {
      handleDelete(id) {
        this.projects = this.projects.filter(item => {
          return item.id !== id
        })
      },
      handelStar(id){
      let p = this.projects.find(item => {
        return item.id === id
      })
      p.star = !p.star
    }
    }
}

</script>
