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
          <td id="name">{{ student.student.name }}</td>
          <td id="email">{{ student.student.email }}</td>
          <td id="street">{{ student.student.address.street }}</td>
          <td id="zip">{{ student.student.address.zipCode}}</td>
          <td id="city">{{ student.student.address.city }}</td>
          <td id="id">{{ student._id}}</td>
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