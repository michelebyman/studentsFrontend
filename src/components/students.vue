<template>
  <div id="students-table">
     <table>
      <tbody>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Street</th>
          <th>City</th>
          <th>Zip code</th>
          <th>Id</th>
        </tr>
        <tr v-for="student in students" :key="student.id">

          <td v-if="editing === student._id">
           <input type="text" v-model="student.student.name" />
        </td>
          <td v-else id="name">{{ student.student.name }}</td>

         <td v-if="editing === student._id">
            <input type="email" v-model="student.student.email" />
          </td>
          <td v-else id="email">{{ student.student.email }}</td>

          <td v-if="editing === student._id">
            <input type="text" v-model="student.student.address.street" />
          </td>
          <td v-else id="street">{{ student.student.address.street }}</td>

          <td v-if="editing === student._id">
             <input type="text" v-model="student.student.address.zipCode" />
          </td>
          <td v-else id="zip">{{ student.student.address.zipCode}}</td>

          <td v-if="editing === student._id">
             <input type="text" v-model="student.student.address.city" />
          </td>
          <td v-else id="city">{{ student.student.address.city }}</td>

          <td id="id">{{ student._id}}</td>

           <td v-if="editing === student._id">
            <button @click="editStudent(student)">Save</button>
            <!-- <button class="muted-button" @click="editing = null">Cancel</button> -->
       </td>
          <td v-else id="button">
            <button id="edit" @click="editMode(student._id)">Edit</button>
          </td>
          <td id="button">
            <button id="delete" @click="$emit('delete:student', student._id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

  export default {
    name: 'students',
    props: {
      students: Array,
    },
    data() {
      return {
        editing: null 
      }
    }, 
    methods: {
      editMode(id) {  
        this.editing = id;
      },
      
      
      editStudent(student){
        this.$emit('edit:student', student._id, student)
        this.editing = null;
      }
    }
  }
</script>

<style scoped>
#name{
  color: black;
  font-weight: bold;
  text-transform: uppercase;
}

th{
  color: black;
  font-weight: bold;
   text-transform: uppercase;
}

#email{
  color: green;
}

#street{
  color: pink;
}

#id, #street, #email, #name, #zip, #city{
  color: black;  
  border: 2px dotted black;
  padding: 10px;
  min-width: 180px;
}

#delete {
  background-color:rgb(136, 0, 0);
  border: none;
  outline: none;
}
#delete:hover {
  background-color: rgb(214, 7, 7);
  transform: scale(1.1)
}

#button{
  border: none;
}


</style>