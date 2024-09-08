<template>
  <div>
    <table class="css-serial">
      <tr>
        <th>Sl. No</th>
        <th>ID</th>
        <th>Dummy Data & TodoList</th>
      </tr>
      <tr v-for="data in dummyData" :key="data.id">
        <td></td>
        <td>{{ data.id }}</td>
        <td>{{ data.title }}</td>
      </tr>
      <tr v-for="item in temp" :key="item.id">
        <td></td>
        <td>{{ item.id }}</td>
        <td>{{ item.title }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Data",

  data() {
    return {
      dummyData: [
        {
          id: 1,
          title: "Dummy Data One",
          completed: false
        },
        {
          id: 2,
          title: "Dummy Data Two",
          completed: false
        },
      ],
      temp: []
    }
  },

  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.temp = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },

}
</script>

<style scoped>
  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #dddddd;
  }

  /* Automatic Serial Number Row */
  .css-serial {
    counter-reset: serial-number;  /* Set the serial number counter to 0 */
  }

  .css-serial td:first-child:before {
    counter-increment: serial-number;  /* Increment the serial number counter */
    content: counter(serial-number);   /* Display the counter */
  }
</style>