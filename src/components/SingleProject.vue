<template>
  <div class="project" :class="{star: project.star  }">
      <div class="actions">
         <table>
          <tr>
            <th><h3 @click="showDetails = !showDetails">{{project.film}} </h3></th>
            <th><p>{{project.director}}</p></th>
            <th>{{project.year}}</th>
          </tr>
        </table>
          <div class="icons">
          <router-link :to="{name: 'EditProject', params:{id:project.id}}">
            <span class="material-icons">edit</span>
          </router-link>
<!--            @click="deleteProject"-->
         <span  @click="deleteProject" class="material-icons ">delete</span>
<!--            @click ="changeComplete" :class="{spanstar: project.star }"-->
         <span  @click ="changeComplete" :class="{spanstar: project.star }"  class="material-icons ">star</span>
        </div>
      </div>
      <div v-if="showDetails " class="details">
        <p>{{project.year}} </p>
      </div>
  </div>

</template>


<script>
import axios from "axios";

export default {
  props: ['project'],
  data() {
    return {
      showDetails: false,
      uri: 'http://127.0.0.1:8000/project/' + this.project.id + '/'
    }
  },
  methods: {
    deleteProject() {
      axios
          .delete(this.uri)
          .then(() => this.$emit('delete', this.project.id))
          .catch(err => console.log(err.message))
    },
    changeComplete() {
      axios({
        method: 'PATCH',
        url: this.uri,
        data: {star: !this.project.star}

        // headers: {'content-Type': 'application/json'},
        // body: JSON.stringify({star: !this.project.star})
      })
          
          .then(()=> this.$emit('star' , this.project.id))
          .catch(err => console.log(err.message))
    }
  }
}
</script>


<style >
.project{
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.5);
  border-left: 4px solid #bbbbbb;
}
h3{
  cursor: pointer;
}
.actions{
  display: flex;
  justify-content: space-between;
  align-items: center;

}
.material-icons{
  font-size: 24px;
  margin-left: 10px;
  color:#bbb;
  cursor: pointer;
}
.material-icons:hover{
  color: #777;
}
.project.star{
    border-left: 4px solid blue;
}
.spanstar{
  color: blue;
}

td, th {
  //border: 1px solid #dddddd;
  text-align: left;
  width: 240px;
}




</style>