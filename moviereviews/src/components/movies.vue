
<template>
    
        <!-- // 9423e2dc9e278efd4886977b8390a54c -->
        <div >
                <div v-if="loading">
                    Loading...
                </div>
                <div v-else>
                    <b-card no-body  >
                        <b-tabs card >
                            <b-tab title="Top Rated Movies" active  >
                                <p class="m-4">Showing <b>{{totalMovies.results.length}}</b> movies of <b>{{totalMovies.total_results}}</b> </p>
                                <div class ="row">
                                                            
                                    <div class="col-md-6 mb-4" v-for="item in topratedMovies" :key="item.id">
                                    
                                        <b-card no-body class="overflow-hidden" style="max-width: 450px;" >
                                            <b-row no-gutters>
                                            <b-col md="6">
                                                <b-card-img :src="'https://image.tmdb.org/t/p/w500/'+item.backdrop_path" alt="Image" class="rounded-0 m-1" style="height:300px;object-fit:none" ></b-card-img>
                                            </b-col>
                                            <b-col md="6">
                                                <b-card-body >
                                                <b-card-text style="font-weight:bold">
                                                    {{item.original_title}}
                                                </b-card-text>
                                                
                                                </b-card-body>
                                                <p style="font-weight:bold">Release Date:  {{item.release_date}}</p>
                                                Vote Average:<b-form-rating inline :value="item.vote_average/2"  disabled></b-form-rating>
                                                <p class="mt-1 mb-1">Vote Count:<b>{{item.vote_count}}</b></p>
                                                <p>Popularity :<b>{{item.popularity}}</b></p>
                                            </b-col>
                                            </b-row>
                                        </b-card>
                                    </div>
                                </div>
                                    <p><b>Page:{{totalMovies.page}}</b></p>
                                <a @click="increasePageCount()" style="cursor:pointer;text-decoration:underline">Show more</a>
                            </b-tab>
                            <b-tab title="Upcoming Movies">
                                    <p class="m-4">Showing <b>{{totalUpcomingMovies.results.length}}</b> movies of <b>{{totalUpcomingMovies.total_results}}</b> </p>
                                <div class ="row">
                                                            
                                    <div class="col-md-6 mb-4" v-for="items in upcomingMovies" :key="items.id">
                                    
                                        <b-card no-body class="overflow-hidden" style="max-width: 450px;" >
                                            <b-row no-gutters>
                                            <b-col md="6">
                                                <b-card-img :src="'https://image.tmdb.org/t/p/w500/'+items.backdrop_path" alt="Image" class="rounded-0 m-1" style="height:300px;object-fit:none" ></b-card-img>
                                            </b-col>
                                            <b-col md="6">
                                                <b-card-body >
                                                <b-card-text style="font-weight:bold">
                                                    {{items.original_title}}
                                                </b-card-text>
                                                
                                                </b-card-body>
                                                <p style="font-weight:bold">Release Date:  {{items.release_date}}</p>
                                                Vote Average:<b-form-rating inline :value="items.vote_average/2"  disabled></b-form-rating>
                                                <p class="mt-1 mb-1">Vote Count:<b>{{items.vote_count}}</b></p>
                                                <p>Popularity :<b>{{items.popularity}}</b></p>
                                            </b-col>
                                            </b-row>
                                        </b-card>
                                    </div>
                                </div>
                                    <p><b>Page:{{totalUpcomingMovies.page}}</b></p>
                                <a @click="increaseUpCount()" style="cursor:pointer;text-decoration:underline">Show more</a>
                            </b-tab>
                        
                        </b-tabs>
                     </b-card>
                </div>
            
        </div>
     
    
</template>
<script>
import 'bootstrap-vue/dist/bootstrap-vue.css'
import axios from "axios";
export default {
    
    data(){
        return{
            topratedMovies:'',
            upcomingMovies:'',
            page:1,
            lpage:1,
            totalMovies:'',
            totalUpcomingMovies:'',
            api_key:"9423e2dc9e278efd4886977b8390a54c",
            loading:true
        }
    },
    mounted(){
       this. getTopratedMovies()
       this.getUpComingMovies()
    },
    methods:{
     async getTopratedMovies(){
         await axios.get("https://api.themoviedb.org/3/movie/top_rated?api_key="+this.api_key+"&page="+this.page).then(res=>{
            this.loading=false;
            this.topratedMovies=res.data.results;
             this.totalMovies=res.data
         })
       },
       increasePageCount(){
           this.page++;
           this.getTopratedMovies()
            document.documentElement.scrollTop = 0; 
       },
        async getUpComingMovies(){
            await axios.get("https://api.themoviedb.org/3/movie/upcoming?api_key="+this.api_key+"&page="+this.lpage).then(
                res=>{
                    console.log(res.data.results)
                    this.loading=false;
                    this.upcomingMovies=res.data.results
                    this.totalUpcomingMovies=res.data
                }
            )
        },
        
        increaseUpCount(){
                        this.lpage++;
            this.getUpComingMovies()
            document.documentElement.scrollTop = 0;
        }
        
       
    }
}
</script>