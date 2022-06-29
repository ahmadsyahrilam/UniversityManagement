<template>
  <h1>Home page</h1>
  <br />
  <hr />
  <br />

  <!-- <form @submit.prevent="getData">
    <input
      type="search"
      v-model="query"
      style="border: solid black 1px; padding: 0.5em"
      placeholder="Search university..."
    />
    <input style="border: solid grey 1px; padding: 0.5em" type="submit" />
  </form>

  {{ universities.name }} -->

  <div style="display: flex; justify-content: center">
    <input
      style="border: solid grey 2px; width: 70%"
      type="text"
      v-model="serach"
      placeholder="Search Universities"
    />
  </div>

  <br />

  <table
    style="
      border-collapse: collapse;
      width: 70%;
      margin-left: auto;
      margin-right: auto;
    "
  >
    <thead>
      <tr>
        <th style="border: 1px solid #dddddd; text-align: left; padding: 8px">
          Name of University
        </th>
        <th style="border: 1px solid #dddddd; text-align: left; padding: 8px">
          URL
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="university in filterUniversity" v-bind:key="university.id">
        <td style="border: 1px solid #dddddd; text-align: left; padding: 8px">
          {{ university.name }}
        </td>
        <td style="border: 1px solid #dddddd; text-align: left; padding: 8px">
          {{ university.domains }}
        </td>
      </tr>
    </tbody>
  </table>

  <!-- working code -->
  <!-- <div>
    <form @submit.prevent="getData">
      <input
        style="border: solid grey 1px; padding: 0.5em"
        type="search"
        v-model="query"
      />
      <input style="border: solid grey 1px; padding: 0.5em" type="submit" />
    </form>
    <ul>
      <li v-for="(item, index) in data" :key="item.id">
        {{ index + 1 }}. {{ item.advice }}
      </li>
    </ul>
  </div> -->
</template>

<script>
import axios from "axios";

export default {
  name: "Home",

  data() {
    return {
      universities: [],
      //searchValue: "",
      query: null,
      //data: [],
      serach: "",
    };
  },

  // methods: {
  //   async getData() {
  //     await axios
  //       .get(`http://universities.hipolabs.com/search?country=Malaysia`)
  //       .then((response) => {
  //         console.log("university name: ", response.data);
  //         this.universities = response.data;
  //       })
  //       .catch((error) => {
  //         console.log(error);
  //       });
  //   },
  // },

  // methods: {
  //   async getData() {
  //     //console.log(this.query);
  //     await axios
  //       .get(`https://api.adviceslip.com/advice/search/${this.query}`)
  //       .then((response) => {
  //         this.data = response.data.slips;
  //         console.log(this.data);
  //       })
  //       .catch((error) => {
  //         console.log(error);
  //       });
  //   },
  // },

  mounted() {
    //GET LIST OF UNIVERSITIES FROM API -> http://universities.hipolabs.com/search?country=Malaysia
    axios
      .get("http://universities.hipolabs.com/search?country=Malaysia")
      .then((response) => {
        console.log("university name: ", response.data);
        this.universities = response.data;

        // console.log(
        //   "domain :",
        //   JSON.parse(JSON.stringify(response.data))
        // );

        //JSON.parse(JSON.stringify(userData))

        //console.log("university name:", response.data[0].name);
      })
      .catch((error) => console.log(error));
  },

  computed: {
    filterUniversity: function () {
      return this.universities.filter((university) => {
        return university.name
          .toLowerCase()
          .includes(this.serach.toLowerCase()); //search includes lowercase
      });
    },
  },

  //  computed: {
  //   resultQuery(){
  //     if(this.searchQuery){
  //     return this.resources.filter((item)=>{
  //       return this.searchQuery.toLowerCase().split(' ').every(v => item.title.toLowerCase().includes(v))
  //     })
  //     }else{
  //       return this.resources;
  //     }
  //   }
  // }
};
</script>