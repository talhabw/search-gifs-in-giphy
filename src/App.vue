<template>
    <div id="app">
        <search @searchRequested="handleSearch"></search>
        <div class="container text-center mt-5 pt-5">
            <h1 v-if="isLoading" class="text-info">LOADING...</h1>
            <h1
                v-else-if="!gifs.length"
                class="text-danger"
            >I couldn't find any gif with your keyword :(</h1>
        </div>
        <preview :gifs="gifs"></preview>
    </div>
</template>

<script>
let apikey = "YOUR_API_KEY";
import Search from "./components/search";
import Preview from "./components/preview";
export default {
    name: "app",
    components: {
        Search,
        Preview
    },
    data() {
        return {
            isLoading: true,
            gifs: []
        };
    },
    methods: {
        doQuery(url) {
            fetch(url)
                .then(res => {
                    return res.json();
                })
                .then(res => {
                    this.gifs = res.data;
                    this.isLoading = false;
                });
        },
        handleSearch(query) {
            if (query != "") {
                this.gifs = [];
                this.isLoading = true;
                let searchUrl = `https://api.giphy.com/v1/gifs/search?api_key=${apikey}&q=${query}`;
                this.doQuery(searchUrl);
            } else if (query == "") {
                let allUrl = `https://api.giphy.com/v1/gifs/trending?api_key=${apikey}`;
                this.doQuery(allUrl);
            }
        }
    },
    created() {
        let url = `https://api.giphy.com/v1/gifs/trending?api_key=${apikey}`;
        this.doQuery(url);
    }
};
</script>

<style>
#app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
</style>
