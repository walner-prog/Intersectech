<template>
  <div class="container">
     <div class="row">
      <div class="col-lg-4 offset-lg-2 mb-3 col-md-8">
        <input type="text" v-model="categoryFilter" class="form-control border-warning fade-in " placeholder="Buscar por título">
      </div>
      <div class="col-lg-2 col-sm-4 mb-3"> <!-- Ajusta las clases de la columna para dispositivos pequeños -->
        <!-- Botón de búsqueda -->
        <button @click="searchPosts" class="btn btn-warning fade-in">Buscar</button>
      </div>
      
     </div>
     <div class="row justify-content-center align-items-center fade-in">
      <div class="col-lg-10  col-sm-12">
        <div class="row">
          <!-- Verifica si hay posts antes de iterar sobre ellos -->
          <template v-if="posts && posts.length > 0">
            <div class="col-md-4" v-for="post in posts" :key="post.id">
              <!-- Contenido de cada post -->
            </div>
          </template>
          <!-- Mensaje si no hay resultados -->
          <template v-else>
            <div class="col-md-12 fade-in">
              <p>No hay resultados de búsqueda.</p>
            </div>
          </template>
        </div>
       </div>
     </div>
  </div>
    
  <div class="row justify-content-center justify-content-center align-items-center fade-in">
    <div class="col-lg-12 col-sm-12">
      <div class="row">
        <div class="col-lg-12">
            <div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel">
                <div class="carousel-inner">
                    <div class="carousel-item active">
                        <img src="https://cdn.computerhoy.com/sites/navi.axelspringer.es/public/media/image/2015/12/139161-que-es-inteligencia-artificial.jpg?tf=1200x" class="d-block w-100" alt="...">
                        <div class="carousel-caption d-none d-md-block text-center text-light">
                            <div class="overlay"></div> <!-- Fondo semitransparente -->
                            <div class="caption-content">
                                <h5>Descubre un Mundo de Conocimiento Tecnológico</h5>
                                <p>En nuestro sitio web, te invitamos a sumergirte en un vasto océano de conocimiento tecnológico.
                                    Ofrecemos una amplia gama de contenido que te mantendrá informado y actualizado en el siempre cambiante mundo de la tecnología. Ya sea que seas un entusiasta tecnológico o simplemente estés interesado en explorar nuevas tendencias,
                                    nuestro sitio es el destino perfecto para satisfacer tu curiosidad y expandir tus horizontes.
                                </p>
                            </div>
                        </div>
                    </div>
                    <div class="carousel-item">
                        <img src="https://www.obicex.es/sites/obicex/files/styles/blog_desktop_webp/public/images/blog/tipos-de-realidad-virtual.jpg.webp?itok=r8uWg1c5" class="d-block w-100" alt="...">
                        <div class="carousel-caption d-none d-md-block text-center text-light">
                            <div class="overlay"></div> <!-- Fondo semitransparente -->
                            <div class="caption-content">
                                <h5>Entendiendo el Futuro Tecnológico</h5>
                                <p>En un mundo donde la tecnología avanza a un ritmo vertiginoso, comprender las tendencias emergentes y sus implicaciones es más crucial que nunca. Nuestro sitio web no solo te ofrece noticias y artículos sobre los últimos desarrollos tecnológicos, 
                                  sino que también te brinda análisis profundos y perspicaces que te ayudarán a comprender el impacto de estas innovaciones en nuestras vidas cotidianas y en el futuro de la sociedad.</p>
                            </div>
                        </div>
                    </div>
                    <div class="carousel-item">
                        <img src="https://f.hubspotusercontent30.net/hubfs/7281139/blog_19-de-enero.jpg" class="d-block w-100" alt="...">
                        <div class="carousel-caption d-none d-md-block text-center text-light">
                            <div class="overlay"></div> <!-- Fondo semitransparente -->
                            <div class="caption-content">
                                <h5>Empoderando tu Conocimiento</h5>
                                <p>En última instancia, nuestro objetivo es empoderarte con el conocimiento que necesitas para tomar decisiones informadas en un mundo cada vez más digitalizado. Creemos en el poder de la educación y la información para transformar vidas y dar forma al futuro. Ya sea que estés buscando tutoriales prácticos sobre cómo utilizar nuevas tecnologías o reflexiones profundas sobre el impacto social de la innovación, 
                                  nuestro sitio web te proporciona las herramientas y los recursos necesarios para mantenerte al tanto y avanzar con confianza en la era digital.</p>
                            </div>
                        </div>
                    </div>
                </div>
                <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="prev">
                    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Previous</span>
                </button>
                <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
                    <span class="carousel-control-next-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Next</span>
                </button>
            </div>
        </div>
    </div>
    
      <br>
      <div class="row fade-in">
        <h3>Aprende sobre diferentes temas.</h3>
        <div class="col-md-4" v-for="post in posts" :key="post.id">
          <div class="card mb-3 ">
            <img :src="post.photo_url" class="card-img-top" alt="Imagen de la publicación">
            <div class="card-body color-card">
              <router-link :to="{ name: 'BlogDetails', params: { id: post.id } }">
                <h5 class="card-title">{{ post.title }}</h5>
              </router-link>
              <p class="card-text text-dark text-opacity-50 fs-6">
                <span class="text-secondary">Author:</span> {{ post.author }} <br>
                <span class="text-secondary">Categoria:</span> {{ post.category }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>

import Swal from 'sweetalert2';
import axios from 'axios';
import slugify from 'slugify'; // Importa la librería para generar slugs
export default {
 
  data() {
    return {
      posts: [],
      categoryFilter: '', // Nueva propiedad para la búsqueda por nombre de usuario
    };
  },
  mounted() {
    this.getUsers();
    this.observeElements();
  },
  methods: {
    async getUsers() {
  try {
    const url = `https://api-blog-v1-1.onrender.com/api/posts?nombre=${this.categoryFilter.trim()}`;
    const response = await axios.get(url);
    this.posts = response.data;
  } catch (error) {
    console.error('Error al obtener los usuarios:', error);
  }
},

searchPosts() {
  // Filtra los posts según el título ingresado por el usuario
  this.posts = this.posts.filter(post => post.title.toLowerCase().includes(this.categoryFilter.toLowerCase()));
},



observeElements() {
      const elements = document.querySelectorAll('.fade-in');
      const observer = new IntersectionObserver(entries => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('fade-in-visible');
            observer.unobserve(entry.target);
          }
        });
      });
      elements.forEach(element => observer.observe(element));
    },

    // Método para buscar usuarios por nombre
    searchUsers() {
      this.getUsers();
    },
    async deleteUser(userId) {
      // Mostrar un mensaje de confirmación con SweetAlert2
      const result = await Swal.fire({
        title: '¿Estás seguro?',
        text: 'No podrás revertir esta acción',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Sí, eliminar'
      });

      // Si el usuario confirma la eliminación
      if (result.isConfirmed) {
        try {
          const response = await axios.delete(`https://apiusuarios-evxn.onrender.com/api/users/${userId}`);
          console.log('Usuario eliminado:', response.data);
          // Mostrar alerta de éxito
          await Swal.fire(
            '¡Eliminado!',
            'El usuario ha sido eliminado correctamente.',
            'success'
          );
          // Actualizar la lista de usuarios después de eliminar uno
          this.getUsers();
        } catch (error) {
          console.error('Error al eliminar el usuario:', error);
          // Mostrar alerta de error
          await Swal.fire(
            'Error',
            'No se pudo eliminar el usuario.',
            'error'
          );
        }
      }
    },
    editUser(userId) {
      // Redirige a la vista de edición del usuario con el ID userId
      this.$router.push({ name: 'EditProcuct', params: { id: userId } });
      console.log('Editando usuario con ID:', userId);
    },
    goToCreateProductView() {
      // Redirige a la vista de creación de usuario
      this.$router.push({ name: 'create-product' });
    },
    
    getPostUrl(post) {
  // Genera el slug a partir del título del post y lo usa en la URL
  const slug = slugify(post.title, { lower: true });
  return `/blog/${slug}`;
  }

  },
};
</script>

<style>
 /* Estilos CSS */
/* Estilos CSS para el fade-in */
.fade-in {
  opacity: 0;
  transition: opacity 1s ease;
}

.fade-in-visible {
  opacity: 1;
}
  /* Estilos CSS para el input */
  .form-control {
    background-color:rgb(255, 237, 205); /* Cambia el color de fondo del input */
    color: white; /* Cambia el color del texto dentro del input */
    border-color:rgb(255, 255, 233) ;/* Cambia el color del borde del input */
  }

  /* Estilos CSS para el botón */
  .btn-orange {
    background-color: orange; /* Cambia el color de fondo del botón */
    border-color: blue; /* Cambia el color del borde del botón */
  }

  /* Cambia el color del texto del botón */
  .btn-orange:hover {
    color: orange;
  }
  .color-card{
    background-color: rgb(251, 186, 66); 
  }
  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
   /* background-color: rgba(0, 0, 0, 0.5); /* Color de fondo semitransparente */
}

.caption-content {
  position: absolute;
  top: 50%; /* Centra verticalmente el contenido */
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1; /* Asegura que el texto esté por encima de la superposición */
  padding: 100px; /* Ajusta el espacio interior según sea necesario */
  width: 80%; /* Ancho del contenido */
  margin-top: -300px;
  color: rgb(255, 196, 0);
  background-color: rgba(0, 12, 116, 0.50); /* Aquí 0.25 representa el nivel de opacidad, puedes ajustarlo según lo necesites */
}


.caption-content h5,
.caption-content p {
    margin: 0; /* Elimina los márgenes predeterminados */
}

</style>


