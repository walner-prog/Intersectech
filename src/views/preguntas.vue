<template>
    <div class="accordion">
      <div v-for="(faq, index) in faqs" :key="index" class="accordion-item" :class="{ 'open': faq.isOpen }">
        <div class="accordion-title" @click="toggleAccordion(index)">{{ faq.question }}</div>
        <div v-if="faq.isOpen" class="accordion-content">{{ faq.answer }}</div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        faqs: [
          {
            question: "¿Cómo puedo crear una cuenta en el blog?",
            answer: "Para crear una cuenta en nuestro blog, simplemente haz clic en el botón 'Registrarse' en la parte superior derecha de la página y sigue las instrucciones.",
            isOpen: false
          },
          // Agrega más preguntas y respuestas aquí
          {
            question: "¿Cuál es la política de moderación de comentarios en el blog?",
            answer: "Nuestra política de moderación de comentarios se centra en mantener un entorno respetuoso y constructivo para todos los usuarios. Los comentarios que contengan lenguaje ofensivo, spam o contenido inapropiado serán eliminados.",
            isOpen: false
          },
          {
  question: "¿Cómo puedo restablecer mi contraseña?",
  answer: "Si olvidaste tu contraseña, puedes restablecerla haciendo clic en '¿Olvidaste tu contraseña?' en la página de inicio de sesión. Te enviaremos un enlace por correo electrónico para que puedas crear una nueva contraseña.",
  isOpen: false
},
{
  question: "¿Qué debo hacer si encuentro un error en el contenido del blog?",
  answer: "Si encuentras algún error en nuestro contenido, como errores tipográficos o información incorrecta, por favor háznoslo saber utilizando nuestro formulario de contacto. Apreciamos tu ayuda para mantener nuestro contenido preciso y actualizado.",
  isOpen: false
},
{
  question: "¿Cómo puedo suscribirme para recibir actualizaciones del blog?",
  answer: "Puedes suscribirte para recibir actualizaciones de nuestro blog introduciendo tu dirección de correo electrónico en el campo de suscripción en la parte inferior de la página. Te enviaremos las últimas publicaciones y noticias directamente a tu bandeja de entrada.",
  isOpen: false
},
{
  question: "¿Cuál es la política de derechos de autor del contenido del blog?",
  answer: "Todo el contenido publicado en nuestro blog está protegido por derechos de autor. No puedes utilizar, copiar o reproducir el contenido sin nuestro permiso explícito. Si estás interesado en utilizar nuestro contenido, por favor contáctanos para obtener más información sobre las licencias.",
  isOpen: false
},
{
  question: "¿Qué temas cubre el blog?",
  answer: "Nuestro blog cubre una amplia variedad de temas relacionados con tecnología, ciencia, negocios, estilo de vida y más. Publicamos regularmente artículos, tutoriales, reseñas y noticias sobre los últimos desarrollos en estos campos.",
  isOpen: false
},
{
  question: "¿Puedo contribuir con contenido al blog?",
  answer: "¡Claro! Si estás interesado en contribuir con contenido a nuestro blog, como artículos, tutoriales o reseñas, por favor ponte en contacto con nosotros a través de nuestro formulario de contacto. Estamos siempre buscando colaboradores talentosos para enriquecer nuestro contenido.",
  isOpen: false
},
{
  question: "¿Cómo puedo reportar un problema técnico en el sitio web?",
  answer: "Si encuentras algún problema técnico mientras navegas por nuestro sitio web, como errores de carga, enlaces rotos o problemas de diseño, por favor repórtalo utilizando nuestro formulario de contacto. Nos esforzamos por proporcionar una experiencia de usuario fluida y tu retroalimentación es muy apreciada.",
  isOpen: false
},
{
  question: "¿Cómo puedo eliminar mi cuenta de usuario?",
  answer: "Si deseas eliminar tu cuenta de usuario en nuestro blog, por favor contáctanos y te ayudaremos con el proceso. Ten en cuenta que una vez eliminada tu cuenta, perderás acceso a todas las funciones y contenido asociados a la misma.",
  isOpen: false
}

        ]
      };
    },
    methods: {
      toggleAccordion(index) {
        this.faqs.forEach((faq, i) => {
          if (i === index) {
            faq.isOpen = !faq.isOpen;
          } else {
            faq.isOpen = false; // Cerrar otros acordeones
          }
        });
      }
    }
  };
  </script>
  
  <style scoped>
  .accordion-item {
    margin-bottom: 15px;
  }
  
  .accordion-title {
    cursor: pointer;
    padding: 10px;
    background-color: #f0f0f0;
  }
  
  .accordion-content {
    padding: 10px;
    display: none;
    background-color: #ffffff;
  }
  
  .accordion-item.open .accordion-content {
    display: block;
  }
  </style>
  