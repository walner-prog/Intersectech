<template>
   
      <section id="about">
        <div class="container">
          <div class="row">
            <div class="col-lg-8 mx-auto text-center">
              <h2 class="section-heading text-orange fade-in">Acerca de Intersectech</h2>
              <hr class="my-4 fade-in">
              <div class="card mb-4 fade-in" style="background-color: rgb(0, 12, 116);">
                <div class="card-body">
                  <p class="card-text text-white mb-4">
                    ¡Bienvenido a <strong>Intersectech</strong>! Soy un desarrollador web apasionado por la tecnología digital y estoy emocionado de compartir este proyecto contigo.
                  </p>
                </div>
              </div>
              <div class="card mb-4 fade-in" style="background-color: rgb(0, 12, 116);">
                <div class="card-body">
                  <p class="card-text text-white mb-4">
                    En <strong>Intersectech</strong>, me esfuerzo por ofrecer contenido educativo y actualizado sobre las últimas tendencias en tecnología y temas tecnológicos que seguro serán de tu interés.
                  </p>
                </div>
              </div>
              <div class="card mb-4 fade-in" style="background-color: rgb(0, 12, 116);">
                <div class="card-body">
                  <p class="card-text text-white mb-4">
                    Siempre estoy explorando nuevas herramientas, técnicas y tendencias en el mundo digital como programador web, y me encanta compartir mis experiencias y descubrimientos con la comunidad de lectores.
                  </p>
                </div>
              </div>
              <div class="card mb-4 fade-in" style="background-color: rgb(0, 12, 116);">
                <div class="card-body">
                  <p class="card-text text-white mb-0">
                    ¿Tienes alguna pregunta, comentario o deseas consultar algo relacionado con el desarrollo web? ¡Me encantaría saber de ti! No dudes en ponerte en contacto a través de mi correo electrónico <a href="mailto:ca140611@gmail.com">ca140611@gmail.com</a> o en nuestras redes sociales.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        
      </section>
      

  </template>
  
  <script>
  import Swal from 'sweetalert2';
  import axios from 'axios';
  
  export default {
    props: {
      posts: {
        type: Array,
        required: true
      }
    },
    methods: {
      async deleteUser(postId) {
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
            const response = await axios.delete(`https://api-blog-v1-1.onrender.com/api/posts/${postId}`);
            console.log('Usuario eliminado:', response.data);
            // Mostrar alerta de éxito
            await Swal.fire(
              '¡Eliminado!',
              'El usuario ha sido eliminado correctamente.',
              'success'
            );
            // Emitir un evento para notificar al componente padre que se ha eliminado un usuario
            this.$emit('user-deleted');
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
        // Emitir un evento para notificar al componente padre que se quiere editar un usuario
        this.$emit('edit-user', postId);
      }
    }
  };

  // Selecciona todos los elementos con la clase "fade-in"
const fadeElements = document.querySelectorAll('.fade-in');

// Opciones para el observador de intersección
const options = {
  root: null,
  rootMargin: '0px',
  threshold: 0.2 // Cambia este valor según tus necesidades
};

// Función de callback para el observador de intersección
const callback = (entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('fade-in'); // Agrega la clase "fade-in" cuando el elemento está visible
      observer.unobserve(entry.target); // Deja de observar el elemento una vez que se ha mostrado
    }
  });
};

// Crea un nuevo observador de intersección con la función de callback y opciones
const observer = new IntersectionObserver(callback, options);

// Observa cada elemento con la clase "fade-in"
fadeElements.forEach(element => {
  observer.observe(element);
});

  </script>
  
  <style>
  /* Estilos CSS */

  @keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  
  .fade-in {
    animation: fade-in 1s ease-in-out forwards;
    opacity: 0; /* Asegura que el contenido esté oculto inicialmente */
  }
  
  .text-orange{
    color: orange;
  }
  </style>
  