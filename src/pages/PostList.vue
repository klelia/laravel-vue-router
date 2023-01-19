<template>
    <section>
    <h1>Lista dei post</h1>
    <div class="row">
            <div class="col-12 col-md-4" v-for="(post, index) in posts" :key="post.id">
                <PostCard :post="post" />
            </div>
    </div>
    <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item" :class="{'disabled': currentPage === 1}">
        <button class="page-link" :disabled="currentPage === 1" @click="getPosts(currentPage - 1)">Previous
        </button>
    </li>
    <li class="page-item" v-for="n in lastPage">
        <button class="page-link" @click="getPosts(n)">{{n}}</button>
    </li> 
    <li class="page-item" :class="{'disabled': currentPage === lastPage}">
        <button class="page-link" :disabled="currentPage === lastPage" @click="getPosts(currentPage + 1)">Next
        </button>
    </li>   
  </ul>
</nav>
    </section>
</template>

<script>
    import axios from 'axios';
    import { store } from '../store';
    import PostCard from '../components/PostCard.vue';
    export default {
        name: 'PostList',
        components: {
            PostCard
        },
        data(){
            return {
                store,
                posts: [],
                currentPage: 1,
                lastPage: null,
                total: 0                
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
            }           
        },
        mounted(){
            this.getPosts(1);
        }
    }
</script>

<style lang="scss" scoped>

</style>