<template>
  <div class="container col-sm-6">
    <nav class="navbar navbar-expand-lg navbar-dark bg-indigo fixed-top">
      <div class="container-fluid">
        <a class="navbar-brand active" href="#"><span class="inter">Inter<span class="sectech">sectech</span></span></a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon text-danger "></span>
        </button>
        <div class="collapse navbar-collapse linknav" id="navbarSupportedContent" ref="navbarCollapse">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item" :class="{ 'active': $route.path === '/home' }" @click="closeNavbar">
              <router-link to="/home" class="nav-link" aria-current="page">Inicio</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/acerca-de' }" @click="closeNavbar">
              <router-link to="/acerca-de" class="nav-link">Acerca de</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/servicio' }" @click="closeNavbar">
              <router-link to="/servicio" class="nav-link">Servicios</router-link>
            </li>
          </ul>
          <div class="row">
            <div class="col-lg-2 col-sm-4 mb-2 tema">
              <button @click="toggleDarkMode" class="btn btn-outline-light ml-2" :class="{ 'active': darkMode }" >
                <i class="fas" :class="{ 'fa-moon': darkMode, 'fa-sun': !darkMode }" @mouseover="toggleHover" @mouseleave="toggleHover"></i>
              </button>
            </div>
            <div class="social-icons col-lg-2 col-sm-4 mb-2"> <!-- Agrega la clase mb-2 para separación -->
              <a href="https://wa.me/50585429144?text=Gracias%20por%20compartir%20informacion%20valiosa%20de%20tecnologia." target="_blank" class="nav-link"><i class="fab fa-whatsapp icons fs-3"></i></a>



              <a href="https://www.facebook.com/Intersectech" target="_blank" class="nav-link "><i class="fab fa-facebook icons fs-3"></i></a>
            </div>
          </div>
          
          <!-- Agrega iconos de WhatsApp y Facebook con enlaces específicos -->
          
        </div>
      </div>
    </nav>
  </div>
  
  <br>
  
  
  <div :class="{ 'dark-theme': isDarkMode }">
    <!-- Contenido de la aplicación -->
    <router-view />
  </div>
  <br><br><br>
  <footer class="footer bg-dark text-light py-4">
    <div class="container">
        <div class="row">
            <div class="col-md-6">
                <h5><span class="inter">Inter</span><span class="sectech">sectech</span></h5>
                <!-- Aquí puedes agregar tu propio logo si lo tienes -->
                <p>Descubre un Mundo de Conocimiento Tecnológico.</p>
            </div>
            <div class="col-md-3">
                <h5>Enlaces</h5>
                <ul class="list-unstyled">
                   
                    <li><a  class=" text-decoration-none enlaces" href="#Copyright">Copyright</a></li>
                    
                   <li> <router-link to="/cookie"  class=" text-decoration-none enlaces" aria-current="page">Cookie policy</router-link></li>
                    
                  
                   <li><router-link to="/preguntas" class=" text-decoration-none enlaces" aria-current="page">Preguntas frecuentes</router-link></li>  

                    <li><a class="text-decoration-none enlaces" href="tel:+50585429144 ">Contacto Intersectech</a></li>

                </ul>
            </div>
            <div class="col-md-3">
                <h5>Suscripciones</h5>
                <p>Inscríbase para recibir actualizaciones por correo electrónico</p>
                <form>
                    <div class="input-group mb-3">
                        <input type="email" class="form-control" placeholder="Correo electrónico" aria-label="Correo electrónico" aria-describedby="basic-addon2">
                        <button class="btn btn-outline-warning" type="button">Suscribirse</button>
                    </div>
                </form>
            </div>
        </div>
        <div class="row mt-4">
            <div class="col-md-6">
                <p>© Reservados todos los derechos</p>
            </div>
            <div class="col-md-6 text-md-end">
              
                <p>Para saber cómo se utilizarán sus datos, consulte nuestro aviso de privacidad.</p>
            </div>
        </div>
    </div>
</footer>
<footer class="footer bg-dark text-light py-4">
  <div class="container">
      <!-- Contenido del footer -->
  </div>
  <div class="container-fluid bg-secondary text-center py-2">
      <p class="mb-0 text-light" id="Copyright">© 2024 Intersectech. Todos los derechos reservados.</p>
  </div>
</footer>


  
  
</template>

<script>
export default {
  data() {
    return {
      darkMode: false,
      isHovered: false
    };
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
      // Aquí puedes agregar la lógica para cambiar el tema
      if (this.darkMode) {
        document.body.classList.add('dark-theme');
      } else {
        document.body.classList.remove('dark-theme');
      }
    },
    toggleHover() {
      this.isHovered = !this.isHovered;
    },
    closeNavbar() {
      // Cierra el menú desplegable cambiando su estado a falso
      this.$refs.navbarCollapse.classList.remove('show');
    }
  }
};

</script>

<style>
/* Estilos para el tema oscuro */
.dark-theme {
  background-color: #1e1e1e;
  color: #fff;
}
.tema{
 margin-right: 100px;
}
.btn-outline-light.active {
  background-color: transparent !important;
}

.fa-moon {
  color: #fff;
}

.fa-sun {
  color: #ffc107;
}

/* Cambiar el color del fondo al pasar el ratón sobre el icono */
.fa-moon:hover,
.fa-sun:hover {
  background-color: #333;
  border-radius: 50%;
}

  .linknav{
    margin-left: 100px;
  }
  .nav-item {
    margin-left: 30px;/* Ajusta el valor según sea necesario */
    color:  orange;
}
.icons{
  color:  orange;
}
.social-icons {
  display: flex;
}
.icons:hover {
 color: aliceblue;
}

.nav-link {
  margin-right: 10px; /* Espacio entre los iconos */
}


  .nav-item.active {
   
    color:  orange;
    border-radius: 25%;
  }
  .bg-indigo{
    background-color: rgb(0, 12, 116);
  }
  .inter{
    font-size: 30px;
    color:white;
    font-weight:bold;
  }
  .sectech{
    font-size: 30px;
    font-weight:bold;
    color: orange;
  }
 
  .nav-item.active {
     
   
    color: orange; 

  }
   .enlaces{
    color:white;
   }
   .enlaces:hover{
    color: orange; 
   }

   .btn-outline-orange:hover{
    color: orange; 
   }

     /* Establece el color y la altura de la línea debajo del enlace */
.nav-link:hover {
  text-decoration: none; /* Quita el subrayado predeterminado */
  position: relative; /* Establece la posición relativa para que el pseudo-elemento esté posicionado correctamente */
}

.nav-link:hover::after {
  content: ""; /* Agrega un contenido al pseudo-elemento */
  position: absolute; /* Establece la posición absoluta para que esté fuera del flujo normal del documento */
  left: 0; /* Coloca el pseudo-elemento al comienzo del enlace */
  bottom: -5px; /* Ajusta la posición vertical de la línea */
  width: 100%; /* Establece el ancho de la línea al ancho completo del enlace */
  height: 2px; /* Establece la altura de la línea */
  background-color: orange; /* Establece el color de la línea */
}
.nav-link.active,
.nav-link:hover {
  background-color: rgba(255, 165, 0, 0.2); /* Cambia el color de fondo al pasar el ratón */
}


  /* Media query para pantallas pequeñas */
  @media (max-width: 992px) {
    .nav-item.active {
     
      padding: 2px; /* Ajusta el padding del elemento de menú activo en pantallas pequeñas */
      width: 80px;
      color: orange; 

    }

    .linknav{
      margin-left: 0px;
    }

    .nav-item {
      margin-left: 0px;/* Ajusta el valor según sea necesario */
  }
  }
</style>
