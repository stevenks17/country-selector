<template>

    <div class="dropdown-container" >
      <h4 class="title">Country State City Dropdown Demo</h4>
        <section v-if="errored">
          <p class="error">We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </section>
      <select class="selector" 
              v-model="selectedCountry" 
              @click="getCountries"
      >
        <option value="">Select a Country</option>
        <option v-for="(country, id) in countries" 
                :key="id"
                :value="country.country_name">
          {{ country.country_name }}
        </option>
      </select>
      <br>

      <select class="selector" 
              v-model="selectedState" 
              @click="getStates"
              :disabled="countries.length === 0"
      >
        <option value="">Select a State</option>
        <option v-for="(state, id) in states" 
                :key="id"
                :value="state.state_name">
          {{ state.state_name }}
        </option>
      </select>
      <br>

      <select class="selector" 
              v-model="selectedCity" 
              @click="getCities" 
              :disabled="states.length === 0"
      >
        <option value="">Select a City</option>
        <option v-for="(city, id) in cities" 
                :key="id"
                :value="city.city_name">
          {{ city.city_name }}
        </option>
      </select>

      <div class="selected">
        "Country": {{ selectedCountry }} 
        "State": {{ selectedState }} 
        "City": {{ selectedCity }}
      </div>

    </div>
</template>

<script>

const axios = require("axios").default;

export default {
  data() {
    return {
        countries: [],
        cities: [],
        states: [],
        selectedCountry: "",
        selectedState: "",
        selectedCity: "",
        city: "",
        token:"",
        errored: false,

      };
    },

     created(){
       this.getToken()
     },

   methods: {

     getToken(){
       axios.get("https://www.universal-tutorial.com/api/getaccesstoken/", {
          headers: {
              "Accept": "application/json",
              "api-token":"zf-MNrWY3vB3QpuyRqBBJafoaNSgPEejxskw4m7EcNWDxnI976PDZaMhIe3srD_SgrY",
              "user-email": "stevenks17@gmail.com"
          }
        }) 
        .then(response => {
          this.token = response.data.auth_token
        })
      },


     
     async getCountries() {
       await axios.get("https://www.universal-tutorial.com/api/countries/", {
          headers: {
              "Authorization": `Bearer ${this.token}`,
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.countries = response.data
        })
        .catch( error => {
          console.log(error)
          this.errored = true
        })
      console.log(this.countries)
    },

     async getStates() {
       await axios.get(`https://www.universal-tutorial.com/api/states/${this.selectedCountry}`, {
          headers: {
              "Authorization": `Bearer ${this.token}`,
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.states = response.data
        })
        .catch( error => {
          console.log(error)
          this.errored = true
        })
        console.log(this.states)
    },

     async getCities() {
       await axios.get(`https://www.universal-tutorial.com/api/cities/${this.selectedState}`, {
          headers: {
              "Authorization": `Bearer ${this.token}`,
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.cities = response.data
        })
        .catch( error => {
          console.log(error)
          this.errored = true
        })

        console.log(this.cities)
    },
  },

}



</script>

<style>
.title {
  font-size: 1.25rem;
  letter-spacing: -.0166573em;
  opacity: 1;
  color: rgba(31, 41, 55, 0.765);
  font-family:Arial, Helvetica, sans-serif;
  font-weight: normal;
  padding-left: 40px;
  height: 4px;
}

.selected {
  color: rgba(124, 65, 212, 0.836);
  display: block;
  margin-top: 3px;
  padding: 10px;
  width: 380px;
  
}

.selector {
  width: 400px;
  border-width: 2px;
  border-radius: 9999px;
  height: 2.5rem;
  padding-left: 5px;
  opacity: 1;
  margin-top: 7px;

}

.error{
  color: red;
  font-weight: bolder;
}
</style>
