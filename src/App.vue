<template>
  <div id="app">
    
    <select class ="country-selector" @click="toggleDropdown">
      <option v-for="country in countries" :key="country.id"> {{ country.name }} </option>
    </select>

    <select class ="state-selector" @click="toggleDropdown">
      <option v-for=" state in countries.states" :key="state.id"> {{ country.state.name }} </option>
    </select>


  </div>
</template>

<script>
// let req = unirest("GET", "https://www.universal-tutorial.com/api/getaccesstoken");

//   req.headers({
//     "Accept": "application/json",
//     "api-token": "zf-MNrWY3vB3QpuyRqBBJafoaNSgPEejxskw4m7EcNWDxnI976PDZaMhIe3srD_SgrY",
//     "user-email": "abc@gmail.com"
//   });
const axios = require('axios').default;
export default{
  data() {
    return {
      active: false,
      countries: [
        {name: 'United States', 
         id: 1,
         states: [
                  {name: 'New York', id: 1},
                  { name: 'Boston', id: 2}
                 ]
        },
        {name: 'United Kingdom', 
         id: 2,
         states: [
                  {name: 'Belfast', id: 1},
                  {name: 'England', id: 2}
                 ]
         },
        {name: 'Europe', id: 3,
         states: [
                  {name: 'Germany', id: 1},
                  {name: 'France', id: 2}
                 ]
        },
      ],
      selectedCountries: null,
      selectedStates: null
    }
  },

  mounted () {
    axios
      .get('https://www.universal-tutorial.com/api/countries/',{
        headers: {
        "Access-Control-Allow-Origin": "*",
        "Accept": "application/json",
        "api-token": "zf-MNrWY3vB3QpuyRqBBJafoaNSgPEejxskw4m7EcNWDxnI976PDZaMhIe3srD_SgrY",
        "user-email": "stevenks17@gmail.com"
        }
      })

      .then(function (response) {
        console.log(response)
      })

      .catch(function (error) {
         console.log(error)
      })
    },


  methods: {
    toggleDropdown() {
      this.active = !this.active
    },

    }
  }

</script>

<style>
.country-selector {

}
</style>
