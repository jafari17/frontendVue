<template>
  <form @submit.prevent="handleSubmit">
    <label>Film:</label>
    <input v-model="film" type="text" required>
    <label>Director:</label>
    <input v-model="director">
    <label>Year:</label>
    <input v-model="year">
    <button>Add Film</button>
  </form>

</template>

<script >
import axios from "axios";

export default {
  data(){
    return{
      film: '',
      director:'',
      year:''
    }
  },
  methods:{
    handleSubmit(){
      let project = {
          film: this.film,
          director: this.director,
          year: this.year,
          star: false,
          slug: "ddddd",
          complete: true,
      }
      console.log(project)

      axios
          .post('http://127.0.0.1:8000/project/', project)
          .then(() => {
            this.$router.push('/')
          } )
          .catch(err => console.log(err.message))

    }

  },

}

</script>



<style >
 form{
   background: white;
   padding: 20px;
   border-radius: 10px;
 }
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input{
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd ;
  width: 100%;
  box-sizing: border-box;
}
textarea{
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button{
  display: block;
  margin: 20px auto 0;
  background: green;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>