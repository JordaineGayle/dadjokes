<template>
    <div>
        <SearchJokes v-on:search-text="searchText"/>
        <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
    </div>
</template>

<script>

import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
    components: {
        Joke,
        SearchJokes
    },
    data() {
        return {
            jokes: []
        }
    },
    async created(){
        var result = await fetch('https://icanhazdadjoke.com/search', {
            headers: {
                Accept: "application/json"
            }
        });
        var data = await result.json();
        this.jokes = data.results;
        console.log(this.jokes);
    },
    methods: {
        searchText: async function(text){
            var result = await fetch('https://icanhazdadjoke.com/search?term='+text, {
                headers: {
                    Accept: "application/json"
                }
            });
            var data = await result.json();
            this.jokes = data.results;
        }
    },
    head(){
        return {
            title: "Dad Jokes",
            meta: [
                {
                    hid: "description",
                    name:"description",
                    content: "Best place for corny dad jokes"
                }
            ]
        }
    }
}
</script>
