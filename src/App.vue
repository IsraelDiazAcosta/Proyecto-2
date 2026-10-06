<script setup>
import{ ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import ButtonCounter from './components/ButtonCounter.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([])

const favorito=ref('')
const postXpagina=10
const inciio=ref(0)
const fin=ref(postXpagina)
const loading=ref(true)

const cambiarFavorito=(post)=>{
  favorito.value=post
}

const next =()=>{
  inciio.value=inciio.value+postXpagina
  fin.value=fin.value+postXpagina
}

const previous =()=>{
  inciio.value=inciio.value-postXpagina
  fin.value=fin.value-postXpagina
}

fetch ('https://jsonplaceholder.typicode.com/posts')
.then((res)=>res.json())
.then((data)=>{posts.value=data})
.finally(()=>{
  setTimeout(()=>{
    loading.value=false
  },2000)
})


</script>

<template>

  <LoadingSpinner v-if="loading">

  </LoadingSpinner>
  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mis post Favorito:{{ favorito }}</h2>

    <PaginatePost 
    @next="next"
    @previous="previous"
    :inicio="inciio"
    :fin="fin"
    :maxLenght="posts.length"
    class="mb-2">
    
  </PaginatePost>
  

    <BlogPost 
    v-for="post in posts.slice(inciio,fin)"
      :key="post.id"
      :id="post.id" 
      :title="post.title" 
      :body="post.body" 
      class="mb-3"

      @cambiarFavoritoNombre="cambiarFavorito"
    ></BlogPost>
    
    
  </div>

</template>