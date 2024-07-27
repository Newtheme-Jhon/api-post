<script setup>

//import ref() variable reactiva
import {ref} from 'vue';

//Import components
import CardPost from './components/CardPost.vue';
import PaginatePost from './components/PaginatePost.vue';

const posts = ref([]);

//paginate posts
const postxpage = 9;
const inicio = ref(0);
const fin = ref(postxpage);

//var progress rectivity
const styleProgress = ref(0);
styleProgress.value = "width:" + fin.value + '%;';

const restApiPosts = async () => {

  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error)
  }

}

//ejecutando la función rest api
restApiPosts();

//functions paginate post
const next = () =>{
  inicio.value = inicio.value + postxpage;
  fin.value = fin.value + postxpage;
  
  if(styleProgress.value >= posts.length){
    styleProgress.value = "width:" + posts.length + '%;';
  }else{
    styleProgress.value = "width:" + fin.value + '%;';
  }
  
  //styleProgress = (styleProgress >= posts.length ? styleProgress : fin.value)
}

const prev = () =>{
  inicio.value = inicio.value - postxpage;
  fin.value = fin.value - postxpage;
  styleProgress.value = "width:" + fin.value + '%;';
}





</script>

<template>
<div class="container-fluid text-center">
  <div class="row">

    <!--title-->
    <div class="col-md-12">
      <h2 class="my-3">API POSTS</h2>
    </div>
    <div class="col-12 d-flex justify-content-center mb-3">
      <PaginatePost 
        @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="posts.length">
      </PaginatePost>
    </div>

    <!--Progres bar-->
    <div class="col-12 my-3">
      <div class="row justify-content-center">
        <div class="w-25">
          <p>{{ (fin > posts.length) ? posts.length : fin }} de {{ posts.length }}</p>
          <div class="progress" role="progressbar" aria-label="Basic example" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">
            <div class="progress-bar" :style="styleProgress"></div>
          </div>
        </div>
      </div>
    </div>
    
    <!--card-post-->
    <div class="col-md-4 py-3 d-flex justify-content-center" v-for="(post, index) in posts.slice(inicio, fin)" :key="index">
      <CardPost 
      :userId="post.userId" 
      :postId="post.id" 
      :title="post.title" 
      :body="post.body"
      ></CardPost>
    </div>

    <div class="col-12 d-flex justify-content-center mb-3">
      <PaginatePost 
        @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="posts.length">
      </PaginatePost>
    </div>

  </div>
</div>
</template>

<style scoped>

</style>
