<script>
import axios from 'axios';

export default {
    name: 'AppMain',
    data(){
        return{
            posts: [],
            loading: false,
            urlAddress: 'http://127.0.0.1:8000/api/posts',
        }
    },
    methods:{
        getPost(){
            axios.get(this.urlAddress, {
                params: {

                }
            })
            .then((response) => {
                this.posts = response.data.results.data;
                console.log(this.posts);
            })
            .catch(function (error) {
                console.log(error);
            })
            .finally(function () {

            }); 
        }
    },
    created(){
        this.getPost();
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-4">
                <h1 class="my-4">
                    Posts:
                </h1>
            </div>
        </div>
        <div class="row g-4">
            <div class="col-sm-6 col-md-4 col-lg-3" v-for="post in posts">
                <article class="card single-post text-center">
                    <div class="card-header fw-bold">
                        {{ post.author }}
                        <br>
                        <span :style="{color: post.type.color}">{{ post.type.name.charAt(0).toUpperCase() + post.type.name.slice(1)}}</span>
                    </div>
                    <img :src="post.image_path" class="card-img-top" :alt="post.title">
                    <div class="card-body">
                        <div class="technologies">
                            <p v-for="tech in post.technologies">
                                <span v-if="post.technologies" class="badge rounded-pill py-2 px-3" :style="{backgroundColor: tech.color}">{{ tech.name }}</span>
                                <span v-else>No technologies</span>
                            </p>
                        </div>
                        <h5 class="card-title">{{post.title}}</h5>
                        <p class="card-text">{{ post.author }}</p>
                        <p class="card-text content">{{ post.content.substr(0, 200) }}...</p>
                        <a href="#" class="btn btn-primary">Read more</a>
                    </div>
                    
                </article>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
   
</style>