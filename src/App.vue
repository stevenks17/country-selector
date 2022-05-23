<template>
  <div id="app">
    <select class="country-selector" v-model="selectedCountry" @click="getCountries">
      <option value="">Select a Country</option>
      <option v-for="(country, id) in countries" 
              :key="id"
              :value="country.country_name">
        {{ country.country_name }}
      </option>
    </select>
    <div>{{ selectedCountry }}</div>

    <select class="state-selector" v-model="selectedState" @click="getStates">
      <option value="">Select a State</option>
      <option v-for="(state, id) in states" 
              :key="id"
              :value="state.state_name">
        {{ state.state_name }}
      </option>
    </select>
    <div>{{ selectedState }}</div>

    <select class="city-selector" v-model="selectedCity" @click="getCities" >
      <option value="">Select a City</option>
      <option v-for="(city, id) in cities" 
              :key="id"
              :value="city.city_name">
        {{ city.city_name }}
      </option>
    </select>
    <div>{{ city.city_name }}</div>

  </div>
</template>

<script>
// let req = unirest("GET", "https://www.universal-tutorial.com/api/getaccesstoken");

//   req.headers({
//     "Accept": "application/json",
//     "api-token": "zf-MNrWY3vB3QpuyRqBBJafoaNSgPEejxskw4m7EcNWDxnI976PDZaMhIe3srD_SgrY",
//     "user-email": "abc@gmail.com"
//   });
const axios = require("axios").default;

export default {
  data() {
    return {
    //   countries: [
    //     {
    //       countryName: "United States",
    //       id: 1,
    //       states: [
    //         {
    //           stateName: "New York",
    //           id: 1,
    //           cities: {
    //             city: "Brooklyn",
    //           },
    //         },
    //         {
    //           stateName: "Massachuesetts",
    //           id: 2,
    //           cities: {
    //             city: "Boston",
    //           },
    //         },
    //       ],
    //     },
    //     {
    //       countryName: "United Kingdom",
    //       id: 2,
    //       states: [
    //         {
    //           stateName: "Belfast",
    //           id: 1,
    //           cities: {
    //             city: "Aberdeen",
    //           },
    //         },
    //         {
    //           stateName: "England",
    //           id: 2,
    //           cities: {
    //             city: "London",
    //           },
    //         },
    //       ],
    //     },
    //     {
    //       countryName: "Europe",
    //       id: 3,
    //       states: [
    //         {
    //           stateName: "Germany",
    //           id: 1,
    //           cities: {
    //             city: "Frankfurt",
    //           },
    //         },
    //         {
    //           stateName: "France",
    //           id: 2,
    //           cities: {
    //             city: "Paris",
    //           },
    //         },
    //       ],
    //     },
    //   ],
        countries: [],
        cities: [],
        states: [],
        selectedCountry: {},
        selectedState: {},
        selectedCity: {},
      };
    },

   methods: {
    // await axios
    //   .get("https://www.universal-tutorial.com/api/getaccesstoken/", {
    //     headers: {
    //       "Accept": "application/json",
    //       "api-token": "zf-MNrWY3vB3QpuyRqBBJafoaNSgPEejxskw4m7EcNWDxnI976PDZaMhIe3srD_SgrY",
    //       "user-email": "stevenks17@gmail.com",
    //     },
    //   })

    //   .then(function (response) {
    //     console.log(response);
    //   })

    //   .catch(function (error) {
    //     console.log(error);
    //   });
    getCountries() {
      axios.get("https://www.universal-tutorial.com/api/countries/", {
          headers: {
              "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJzdGV2ZW5rczE3QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6InpmLU1OcldZM3ZCM1FwdXlScUJCSmFmb2FOU2dQRWVqeHNrdzRtN0VjTldEeG5JOTc2UERaYU1oSWUzc3JEX1NnclkifSwiZXhwIjoxNjUzNDI4NTM2fQ.-Ac9CIzmNcpifUSqrkKqTpVeKpMcoKQcS_bif8fs_Kk",
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.countries = response.data
        })
        console.log(this.countries)
    },

    getStates() {
      axios.get(`https://www.universal-tutorial.com/api/states/${this.selectedCountry}`, {
          headers: {
              "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJzdGV2ZW5rczE3QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6InpmLU1OcldZM3ZCM1FwdXlScUJCSmFmb2FOU2dQRWVqeHNrdzRtN0VjTldEeG5JOTc2UERaYU1oSWUzc3JEX1NnclkifSwiZXhwIjoxNjUzNDI4NTM2fQ.-Ac9CIzmNcpifUSqrkKqTpVeKpMcoKQcS_bif8fs_Kk",
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.states = response.data
        })
        console.log(this.states)
    },

    getCities() {
      axios.get(`https://www.universal-tutorial.com/api/cities/${this.selectedState}`, {
          headers: {
              "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJzdGV2ZW5rczE3QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6InpmLU1OcldZM3ZCM1FwdXlScUJCSmFmb2FOU2dQRWVqeHNrdzRtN0VjTldEeG5JOTc2UERaYU1oSWUzc3JEX1NnclkifSwiZXhwIjoxNjUzNDI4NTM2fQ.-Ac9CIzmNcpifUSqrkKqTpVeKpMcoKQcS_bif8fs_Kk",
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.cities = response.data
        })
        console.log(this.cities)
    },
  },

}



</script>

<style>
.country-selector {
  width: 500px;
}
.state-selector {
  width: 500px;
}

.city-selector {
  width: 500px;
}
</style>
