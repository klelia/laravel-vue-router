<template>
    <section class="contact_me py-5">
        <div class="inner-wrapper">
            <div class="container-fluid text-center">
                <h2 class="text-uppercase">contact me</h2>                
                <div class="row">
                    <form class="col-12 text-start">
                        <div class="mb-3">
                            <input class="border-0 border-bottom form-control" 
                                type="text" name="name" id="name" placeholder="Name">
                        </div>
                        <div class="mb-3">
                            <input class="border-0 border-bottom form-control" 
                                type="text" name="email" id="email" placeholder="Email">
                        </div>
                        <div class="mb-3">
                            <textarea class="border-0 border-bottom form-control"
                               name="message" id="message" cols="30"
                                rows="10" placeholder="Message"></textarea>
                        </div>
                        <button class="btn btn-lg btn-primary text-white" type="submit" >Send</button>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios';
import {store} from '../store';
    export default {
        name: 'ContactForm',
        data(){
            return {
                store,
                name: '',
                email: '',
                message: '',
                success: false,
                errors: {}
            }
        },
        methods: {
            sendForm(){
                const data = {
                    name: this.name,
                    email: this.email,
                    message: this.message
                }
                axios.post(`${this.store.apiBaseUrl}/contacts`, data).then((response)=>{
                    console.log(response.data);
                });
            }
        }

    }
</script>

<style lang="scss" scoped>

</style>