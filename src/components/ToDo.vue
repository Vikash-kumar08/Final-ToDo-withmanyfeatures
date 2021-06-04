<template>
  <div>
    <nav>  
    <h> ToDo List</h>
    </nav>
    <table border="2px" align="center">
        <tr>
            <td>ToDo_name</td>
            <td>ToDo_time</td>
            <td>Action</td>
            <td><button>Delete</button></td>
        </tr>
        <tr v-for = "todo in todolist" v-bind:key="todo.id">
            <td>{{todo.todo_name}}</td>
            <td>{{todo.todo_time}}</td>
            <td><input type="checkbox"/></td>
            <td><button>Delete</button></td>
        </tr>
    </table>
    <br><br>

   <h>AddToDo</h>
    <!-- <form v-on:submit="addToDo">
      <input type="text" v-model="post.name" placeholder="Product Name" />
      <input type="number" v-model="post.price" placeholder="Price" />
      <button type="submit">Add</button>
    </form> -->

    <form @submit="addToDo">
      <input type="text" placeholder="todo_name" />
      <input type="text" placeholder="todo_time" />
      <button type="submit">Add</button>
    </form> 
  </div>
</template>



<script>
export default {
  name: "ToDo",

  data: function () {
    return {
      todolist: [
                 { todo_name:"bathing" , todo_time:"7:30"},
                 { todo_name:"yoga" , todo_time:"8:30"},
                 { todo_name:"rest" , todo_time:"9:00"},
                 { todo_name:"breakfast" , todo_time:"9:15"},
                 { todo_name:"study" , todo_time:"10:00"}
                ]
    };
  },
  methods: {
    addToDo(e) {
    
      e.preventDefault(); // it prevent from page reload
    }
  }
}
</script>
