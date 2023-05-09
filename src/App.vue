<script setup>
import { computed, ref, onMounted } from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

//import ButtonCounter from  './components/ButtonCounter.vue'
// const posts = ref([
//   {title: 'Post 1', id:1, body: 'descripcion 1'},
//   {title: 'Post 2', id:2, body: 'descripcion 2'},
//   {title: 'Post 3', id:3, body: 'descripcion 3'},
//   {title: 'Post 4', id:4},

// ]) borramos porque son datos estaticos y queremos dinamicos
const posts = ref([]);
const postXpage = 10; //¿cuantos elementos pintar en el sitio web?
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorito = ref('');

const cambiarFavorito = (title) =>{
  favorito.value = title;
};

const next = ()=>{
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage
  
 
}

const prev = ()=>{
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage
  //fin.value +=-postXpage
 
}

// onMounted(async()=>{
//   //loading.value = true;
//   try { //try y catch para capturar los errores
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//     posts.value = await res.json()
//   } catch(error) {
//     console.log(error);
//   } finally {
//     setTimeout(()=>{
//         loading.value=false
//     },2000);
//   }

// });



//   fetch('https://jsonplaceholder.typicode.com/posts')//data que obtenemos de nuestra API externa.
//     .then(res => res.json())
//     .then(data=>{posts.value=data})

//     .catch(e => console.log(e))  .....captura un error
//     .finally(() => {
//       setTimeout(()=>{
//         loading.value=false
//       },2000);
//     }); 
  

const fetchDAata = async () =>{

  try { 
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch(error) {
    console.log(error);
  } finally {
    setTimeout(()=>{
        loading.value=false
    },2000);
  }


};

fetchDAata();




const maxlength = computed( () => posts.value.length)
</script>

<template>

  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else > 
    <h1>APP</h1>
    <h2>Mis Posts favoritos: {{favorito }}</h2>


    <PaginatePost 
      @next="next" 
      @prev="prev"
      :inicio="inicio"
      :fin="fin"
      :maxlength="maxlength"
      class="mb-2" /> 

    <BlogPost 
        v-for = "post in posts.slice(inicio, fin)"
        :key="post.id" 
        :title="post.title" 
        :id="post.id"
        :body="post.body"
        @cambiarFavoritoNombre="cambiarFavorito" 
        
        class="mb-2"
    ></BlogPost>
  </div>
</template>


      <!-- <ButtonCounter></ButtonCounter>
    <button-counter></button-counter> -->

    <!-- <BlogPost title="Post 1" id="1" body="descripcion 1" colorText="primary"></BlogPost>
    <BlogPost title="Post 2" id="2" body="descripcion 2" colorText="secondary"></BlogPost>
    <BlogPost title="Post 3" id="3" body="descripcion 3" colorText="success"></BlogPost>
    <BlogPost title="Post 4" id="4" body="descripcion 4" colorText="primary"></BlogPost> -->

  <!-- <BlogPost title="Post 1" :id="1" body="descripcion 1"/>
  <BlogPost title="Post 2" :id="2" body="descripcion 2"/>
  <BlogPost title="Post 3" :id="3" body="descripcion 3"/>
  <BlogPost title="Post 4" :id="4" body="descripcion 4"/>  Se tiene que poner los 2 puntospara que lea NUmber-->