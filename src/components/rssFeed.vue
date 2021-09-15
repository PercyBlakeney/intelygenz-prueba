<template>
    <b-container>
        <h3>Rss Movies Feed:</h3>
        <b-row class="mt-5 mb-5">
            <b-col>
                <b-form-input v-model="searchMovie" placeholder="Buscar Pelicula" v-on:keyup="findMovie"> </b-form-input>
            </b-col>
            <b-col>
                <b-button-group>            
                    <b-button variant="primary" @click="orderMoviesByYear">Order by Year</b-button>
                    <b-button variant="primary" @click="orderMoviesByTitle">Order by Title</b-button>
                    <b-button variant="primary" @click="orderMoviesByScore">Order by Score</b-button>
                </b-button-group>
            </b-col>
        </b-row>
        
        <b-list-group style="text-align: left;">
            <b-list-group-item v-for="item in moviesList" :key="item.imdbID">
                <b-row>
                    <b-col><b-img :src="item.Poster" width="80" alt="placeholder"></b-img></b-col>
                    <b-col cols="10">
                        <h5 class="mt-0 mb-1">{{ item.Title }} <b>({{item.Year}})</b> <i> Score: ({{item.Metascore}})</i></h5>
                        <p class="mb-0">
                            {{ item.Plot }}
                        </p>
                        <b-button variant="outline-primary" class="mt-2" v-b-modal.moreData @click="updateInfoData(item)">Mas info</b-button>
                    </b-col>
                </b-row>
            </b-list-group-item>
        </b-list-group>

        <b-modal id="moreData" :title="title" hide-footer>
            <b-row>
                <b-col>
                    <b-img :src="poster" width="220"></b-img>
                </b-col>
                <b-col>
                    <p><b>plot:</b> {{plot}}</p>
                    <p><b>score:</b> {{score}}</p>
                    <p><b>genre:</b> {{genre}}</p>
                    <p><b>year:</b> {{year}}</p>
                    <p><b>actors:</b> {{actors}}</p>
                    <p><b>boxOffice:</b> {{boxOffice}}</p>
                    <p><b>country:</b> {{country}}</p>
                </b-col>
            </b-row>
        </b-modal>
        
    </b-container>
</template>
<script>
    import axios from 'axios';
    export default {
        name: 'rssFeed',
        data() {
            return {

                //modal Data
                title:"",
                plot:"",
                score:"",
                genre:"",
                year:"",
                actors:"",
                boxOffice:"",
                country:"",
                poster:"",

                //list Data
                rssData: [],
                moviesList: [],
                searchMovie: ""
            };
        },
        created: function() {
            for (var i = 0; i < 11; i++) {
                var letter = null
                var characters = 'ADEIJNSTUWYZadehijnstuyz';
                letter = characters.charAt(i);
                axios
                .get('http://www.omdbapi.com/?i=tt3896198&apikey=af67d4e6&', {
                    params: {
                        t: letter
                    }
                })
                .then(res => {
                    try{
                        this.rssData.push(res.data)
                    }catch(e){
                        console.log(e)
                    }
                    this.orderMoviesByYear()
                    this.moviesList = this.rssData
                })
            }
            
        },
        methods: {
            findMovie: function () {
                this.moviesList = this.rssData.filter( data => data.Title.includes(this.searchMovie))
            },
            updateInfoData: function(item) {
                this.title = item.Title
                this.plot = item.Plot
                this.score = item.Metascore
                this.genre = item.Genre
                this.year = item.Year
                this.actors = item.Actors
                this.boxOffice = item.BoxOffice
                this.country = item.Country
                this.poster = item.Poster
            },
            orderMoviesByYear: function() {
                this.moviesList.sort((a,b) => (a.Year > b.Year) ? 1 : ((b.Year > a.Year) ? -1 : 0));
            },
            orderMoviesByTitle: function() {
                this.moviesList.sort((a,b) => (a.Title > b.Title) ? 1 : ((b.Title > a.Title) ? -1 : 0));
            },
            orderMoviesByScore: function() {
                this.moviesList.sort((a,b) => (a.Metascore > b.Metascore) ? 1 : ((b.Metascore > a.Metascore) ? -1 : 0));
            }
        }
    }
</script>

<style>
    p {
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2; /* number of lines to show */
        line-height: X;
        max-height: X*2;
    }

    .container {
        max-width: 720px;
    }
</style>