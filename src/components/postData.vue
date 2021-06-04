<template>
  <div>
   <h> List of Data</h>
  <form v-on:submit="addProduct" method="post">
        <input type="text" v-model="post.name" placeholder="Product Name" >
        <input type="number"  v-model="post.price"  placeholder="Price" >
        <button type="submit">Add</button>
      </form>
</div>


</template>



<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios,axios)
 export default {
     name:"postData",

     data: function(){
     return {
      post:{name: "",
       price: "",
     }
   }
},
 methods: {
    addProduct(e){

      this.axios.post('http://localhost:8080',this.post).then((result)=>{
        console.warn(result)
      })
      e.preventDefault() // it prevent from page reload
      // console.log(this.name, this.price);
    }
  }


 }


</script>
