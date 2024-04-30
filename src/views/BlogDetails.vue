
<template>
 
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-12">
        <div>
          <h2>{{ post.title }}</h2>
         
          <img :src="post.photo_url" alt="Imagen de la publicación" style="max-width: 100%; height: auto;">
          <p class="card-text text-dark text-opacity-50 fs-6">
            <span class="text-secondary">Author:</span> {{ post.author }} <br>
            <span class="text-secondary">Categoria:</span> {{ post.category }}
          </p>
          <br><br>
          <div v-if="post.content">
            <p v-for="(paragraph, index) in post.content.split('\n')" :key="index">
              <!-- Si el párrafo comienza con un carácter específico, lo tratamos como un subtítulo -->
              <template v-if="paragraph.startsWith('#')">
                <h3>{{ paragraph.slice(1) }}</h3>
              </template>
              <!-- Si no, simplemente mostramos el texto del párrafo -->
              <template v-else>
                {{ paragraph }}
              </template>
            </p>
          </div>
        </div>
      </div>
      <div class="col-lg-4 col-md-12">
        <br><br><br><br>
      
        <!-- Filtra los posts relacionados basados en la misma categoría que el post actual -->
        <div v-if="post">
          <h3>Contenido relacionado</h3>
          <div v-for="relatedPost in posts.filter(p => p.category === post.category && p.id !== post.id)" :key="relatedPost.id">
            <img :src="relatedPost.photo_url" alt="Imagen del post relacionado" style="max-width: 100%;">
            <!-- Utiliza router-link para navegar al detalle del post relacionado -->
            <router-link :to="{ name: 'BlogDetails', params: { id: relatedPost.id } }">{{ relatedPost.title }}</router-link>
            <hr>
          </div>
        
        </div>
      </div>
    </div>
  </div>
  
  </template>
  <script>
import axios from 'axios';

export default {
  data() {
    return {
      post: null,
      posts: [] // Agrega una propiedad para almacenar la lista completa de posts
    };
  },
  created() {
    const postId = this.$route.params.id;
    this.fetchPostDetails(postId);
    this.fetchAllPosts(); // Llama a la función para obtener todos los posts
  },
  watch: {
    '$route.params.id': function(newPostId) {
      // Cuando cambia el ID de la ruta, volvemos a cargar los detalles del post
      this.fetchPostDetails(newPostId);
    }
  },
  methods: {
    async fetchPostDetails(postId) {
      try {
        const response = await axios.get(`https://api-blog-v1-1.onrender.com/api/posts/${postId}`);
        this.post = response.data;
      } catch (error) {
        console.error('Error al obtener los detalles de la publicación:', error);
      }
    },
    async fetchAllPosts() {
      try {
        const response = await axios.get(`https://api-blog-v1-1.onrender.com/api/posts`);
        this.posts = response.data; // Almacena la lista completa de posts en this.posts
      } catch (error) {
        console.error('Error al obtener todos los posts:', error);
      }
    }
  }
};
</script>

  
  <style>
  /* Estilos CSS para el componente BlogDetails */
  </style>