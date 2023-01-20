<template>
   <section v-if="post">
   <h1>{{ post.title }}</h1>
   <img :src="`${store.imagBasePath}${post.cover_image}`" class="card-img-top" :alt="post.title">
   <p>{{ post.content }}</p>
   <div v-if="post.category">
    <h5>Category: {{ post.category.name }}</h5>
   </div>
   <div v-if="post.tags && post.tags.length > 0">
    <h5>Tags</h5>
    <div>
        <span v-for="(tag,index) in post.tags" :key="index" class="badge text-bg-info">{{ tag.name }}</span>
    </div>
   </div>
   </section>
   <section v-else>Loading...</section>
</template>

<script>
    import axios from 'axios';
    import { store } from '../store';
    export default {
        name: 'SinglePost',
        data(){
            return {
                store,
                post: null,
            }
        },
        methods:{
            getPost(){
                console.log(this.$route);
                 axios.get(`${this.store.apiBaseUrl}/posts/${this.$route.params.slug}`).then((response)=>{
                    //console.log(response.data.results);
                    if(response.data.success){
                        //console.log(response.data.results);
                        this.post = response.data.results;
                    } else {
                        //console.log(this.$router);
                        this.$router.push({name: 'not-found'});
                    }
                   
                });         

            }
        },
        mounted(){
        //     this.$watch(() => this.$route.params, (toParams, previousParams) => {
        //  if(toParams !== previousParams){
            this.getPost();
        //      }
        //   }
        // )
  },
            
        }
        

</script>

<style lang="scss" scoped>

</style>