<template>
    <div class="card" style="width: 18rem;">
                    <img :src="`${store.imagBasePath}${post.cover_image}`" class="card-img-top" :alt="post.title">
                    <div class="card-body">
                        <h5 class="card-title">{{post.title}}</h5>
                        <p class="card-text">{{ truncateContent }}</p>
                        <router-link class="btn btn-primary" :to="{name: 'single-post', params:{slug: post.slug}}">
                        Vedi il post
                        </router-link>                    
                    </div>
                </div>
</template>

<script>
import {store} from '../store';
    export default {
        name: 'PostCard',
        props: ['post'],
        data(){
            return {
                store,
                contentMaxLen: 100

            }
        },
        computed:{
            truncateContent(){
                if(this.post.content.length > this.contentMaxLen){
                    return this.post.content.substr(0,this.contentMaxLen) + '...';
                }
                return this.post.content;            
            }
        }
        
    }
</script>

<style lang="scss" scoped>

</style>