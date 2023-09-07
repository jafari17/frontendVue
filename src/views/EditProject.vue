<template>
  <form @submit.prevent="handleEdit" >
    <label>Film:</label>
    <input v-model="film" type="text" required>
    <label>Director:</label>
    <input v-model="director">
    <label>Year:</label>
    <input v-model="year">
    <button>Update Film</button>
  </form>
</template>

<script >
import axios from "axios";

export default {
  props: ['id'],
  data() {
    return {
      film: '',
      director: '',
      year:'',
      uri: "http://127.0.0.1:8000/project/" + this.id +'/',

      project:[]
    }
  },
  mounted() {
        axios
        .get(this.uri )
        .then(response => {
          let data = response.data
          this.project = data
          this.film = data.film
          this.director = data.director
          this.year = data.year
          console.log(this.project )
        }).catch(err => console.log(err.message))
  },

  methods: {
    // handleEdit(){
    //   fetch(this.uri,{
    //     method:"PATCH",
    //     headers:{ 'content-Type': 'application/json'},
    //     body: JSON.stringify({film: this.film , director:this.director, year:this.year})
    //   }).then(() => {
    //      this.$router.push('/')
    //   }).catch(err => console.log(err.message))
    // }


    handleEdit(){
       let project = {
          film: this.film,
          director: this.director,
          year: this.year,
      }
      console.log(project)

      axios
          .patch(this.uri   , project )
          .then(() => {
            this.$router.push('/')
          } )
          .catch(err => console.log(err.message))

    }



    // handleEdit() {
    //
    //   axios({
    //     method: 'PATCH',
    //     url: this.uri + ,
    //     id:this.id,
    //     data: {
    //       film: this.film,
    //       director: this.director,
    //       year: this.year,
    //     }
    //   })
    // }



  }

}
</script>


<style scoped>

</style>