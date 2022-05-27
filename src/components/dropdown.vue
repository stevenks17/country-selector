<template>

    <div class="dropdown-container" >
      <h4 class="title">{{ title }}</h4>
      <select class="selector" 
              @change="$emit('fetch', $event)"
 
      >
        <option value="">Select a {{ defaultValue }}</option>
        <option v-for="(option, id) in options" 
                :key="id"
                :value="option.value"
                >
          {{ option.value }}
        </option>
      </select>
      <br>
    </div>
</template>

<script>


export default {
  props:{
    title: String,
    options: Array,
    selectedOption: String,
    defaultValue: String

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
