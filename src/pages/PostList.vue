<template>
    <section>
    <h1>Lista dei post</h1>
    <div class="row">
            <div class="col-12 col-md-4" v-for="(post, index) in posts" :key="index">
                <div class="card" style="width: 18rem;">
                    <img :src="`${store.imagBasePath}${post.cover_image}`" class="card-img-top" :alt="post.title">
                    <div class="card-body">
                        <h5 class="card-title">{{post.title}}</h5>
                        <p class="card-text">{{ truncateContent(post.content) }}</p>
                        <router-link class="btn btn-primary" :to="{name: 'single-post', params:{slug: post.slug}}">
                        Vedi il post
                        </router-link>                    
                    </div>
                </div>
            </div>
    </div>
    <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item" v-for="n in lastPage"><a class="page-link" @click="getPosts(n)">{{n}}</a></li>    
  </ul>
</nav>
    </section>
</template>

<script>
    import axios from 'axios';
    import { store } from '../store';
    export default {
        name: 'PostList',
        data(){
            return {
                store,
                posts: [],
                currentPage: 1,
                lastPage: null,
                total: 0,
                contentMaxLen: 100
            }
        },
        methods:{
            getPosts(pagenum){
                axios.get(`${this.store.apiBaseUrl}/posts`,{params:{
                   page: pagenum 
                }}).then((response)=>{
                    //console.log(response.data.results);
                   this.posts = response.data.results.data;
                   this.currentPage = response.data.results.current_page;
                   this.lastPage = response.data.results.last_page;
                   this.total = response.data.results.total;
                })
            },
           truncateContent(text){
            if(text.length > this.contentMaxLen){
                return text.substr(0,this.contentMaxLen) + '...';
            }
            return text;
           }
        },
        mounted(){
            this.getPosts(1);
        }
    }
</script>

<style lang="scss" scoped>

</style>