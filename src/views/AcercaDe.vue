<template>
   
      <section id="about">
        <div class="container">
          <div class="row">
            <div class="col-lg-8 mx-auto text-center">
              <h2 class="section-heading">Acerca de Intersectech</h2>
              <hr class="my-4">
              <p class="mb-4">
                ¡Bienvenido a <strong>Intersectech</strong>! Soy un desarrollador web apasionados por la tecnología digital y estoy emocionados de compartir este  proyecto contigo.
              </p>
              <p class="mb-4">
                En <strong>Intersectech</strong>, me  esfuerzo por ofrecer contenido educativo y actualizado sobre las últimas tendencias acerca de la  tecnología en general y temas tecnológicos que seguro seran de tu interes.
              </p>
              <p class="mb-4">
                Siempre estoy explorando nuevas herramientas, técnicas y tendencias en el mundo digital como programador web, y me encanta compartir mis experiencias y descubrimientos con la  comunidad de lectores.
              </p>
              <p class="mb-4">
                ¿Tienes alguna pregunta, comentario o consultar algo referente al desarrollo web ? ¡me  encantaría saber de ti! No dudes en ponerte en contacto  a través de mi correo electrónico <a href="mailto:ca140611@gmail.com">ca140611@gmail.com</a> o en nuestras redes sociales.
              </p>
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
  </script>
  
  <style>
  /* Estilos CSS */
  </style>
  