<template>
  <div>
      <p><nuxt-link to="/jokes">Back</nuxt-link></p>
      <img :src="'https://icanhazdadjoke.com/j/'+$route.params.id+'.png'"  alt="no image"/>
      
        <hr/>
      <small>Joke ID: {{$route.params.id}}</small>
  </div>
</template>

<script>

export default {
    async created() {
        var result = await fetch('https://icanhazdadjoke.com/search', {
            headers: {
                Accept: "application/json"
            }
        });
    },
    data(){
        return {
            joke: {}
        }
    }
}
</script>

<style>

</style>