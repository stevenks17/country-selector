<template>
  <div id="app">
        <section v-if="errored">
          <p class="error">We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </section>
    <dropdown
      title="Country State City Dropdown Demo"  
      :selectedOption="selectedCountry"
      :options="countries"
      @fetch="fetchStates"
      defaultValue="Country"
    />

    <dropdown  
      :selectedOption="selectedState"
      :options="states"
      @fetch="fetchCities"
      defaultValue="State"


    />

    <dropdown  
      :selectedOption="selectedCity"
      :options="cities"
      defaultValue="City"
      @fetch="selectedCity = $event.target.value"
    />

    <div>
      Country: {{ selectedCountry }} 
    </div>

    
    <div>
      State: {{ selectedState }} 
    </div>
    
    <div>
      City: {{ selectedCity }} 
    </div>
  </div>


</template>

<script>
import dropdown from './components/dropdown.vue'

const axios = require("axios").default;

export default {

  components: { 
    dropdown
  },

  data(){
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
    }

  },

     created(){
       this.getToken()
            .then(()=> this.fetchCountries() )
      
    },
  methods: {
    getToken(){
    return   axios.get("https://www.universal-tutorial.com/api/getaccesstoken/", {
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
     fetchCountries() {
       axios.get("https://www.universal-tutorial.com/api/countries/", {
        headers: {
            "Authorization": `Bearer ${this.token}`,
            "Accept": "application/json"
        }
      }) 
      .then(response => {
        this.countries = response.data.map( country => ({value:country.country_name}))
      })
      .catch( error => {
        console.log(error)
        this.errored = true
      })


    },
       fetchStates(event) {
         this.selectedCountry = event.target.value

        axios.get(`https://www.universal-tutorial.com/api/states/${event.target.value}`, {
          headers: {
              "Authorization": `Bearer ${this.token}`,
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.states = response.data.map( state => ({value:state.state_name}))

        })
        .catch( error => {
          console.log(error)
          this.errored = true
        })
        console.log(this.states)

    },
      fetchCities(event) {
        this.selectedState = event.target.value
        axios.get(`https://www.universal-tutorial.com/api/cities/${event.target.value}`, {
          headers: {
              "Authorization": `Bearer ${this.token}`,
              "Accept": "application/json"
          }
        }) 
        .then(response => {
          this.cities = response.data.map( country => ({value:country.city_name}))
        })
        .catch( error => {
          console.log(error)
          this.errored = true
        })

        console.log(this.cities)
    },
  }
}

</script>

<style>
</style>
