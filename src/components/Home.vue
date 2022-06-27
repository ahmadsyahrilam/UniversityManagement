<template>
  <h1>Home page</h1>
  <br />
  <hr />
  <br />
  <input
    style="border: solid black 1px"
    v-model.trim="search"
    placeholder="Search university..."
    @keyup="getUniList"
  />
  <div class="item error" v-if="input && !filteredList().length">
    <p>No results found!</p>
  </div>

  <br />
  <table class="table-auto">
    <thead>
      <tr>
        <th>Name of University</th>
        <th>URL</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="university in universities" v-bind:key="university.id">
        <td>{{ university.name }}</td>
        <td>{{ university.domains }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",

  data() {
    return {
      universities: [],
    };
  },

  mounted() {
    //GET LIST OF UNIVERSITIES FROM API -> http://universities.hipolabs.com/search?country=Malaysia
    axios
      .get("http://universities.hipolabs.com/search?country=Malaysia")
      .then((response) => {
        console.log("university name: ", response.data);
        this.universities = response.data;
        //console.log("university name:", response.data[0].name);
      })
      .catch((error) => console.log(error));
  },
};
</script>