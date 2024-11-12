<template>
  <div id="app">
    <!-- Barra de navegación con enlaces a diferentes rutas -->
    <nav class="navbar">
      <!-- Logo o ícono de Vue en la esquina izquierda con el enlace a "Home" -->
      <router-link to="/" class="navbar-brand" style="text-decoration: none;">
        <img src="https://upload.wikimedia.org/wikipedia/commons/f/f1/Vue.png" alt="Vue Logo" class="logo" />
        <span class="brand-name">Gestor de Tareas</span>
      </router-link>
      <!-- Enlaces de navegación -->
      <div class="nav-links">
        <router-link to="/Addtask">Agregar Tarea</router-link>
        <router-link to="/Tasklist">Lista de Tareas</router-link>
        <router-link to="/Combinedview">Vista Combinada</router-link>
      </div>
    </nav>
    <!-- Aquí se cargará el componente correspondiente a la ruta seleccionada -->
    <router-view />
  </div>
</template>


<style>
/* Mantener el color blanco del texto en navbar-brand */
.navbar-brand {
  display: flex;
  align-items: center;
  color: white; /* Asegura que el texto sea blanco */
  text-decoration: none; /* Elimina el subrayado del enlace */
}

/* Asegúrate de que el texto no cambie de color al estar activo */
.navbar-brand:hover,
.navbar-brand:focus,
.navbar-brand.router-link-active {
  color: white; /* Mantiene el color blanco al pasar el mouse o al estar activo */
}

/* Resto de tu CSS permanece igual */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

/* Estilos para el navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #3bb3ad; /* Fondo azul */
  padding: 15px 30px;
  color: white;
}

/* Logo y nombre de la marca */
.logo {
  width: 40px; /* Ajusta el tamaño del logo según sea necesario */
  margin-right: 10px;
}

.brand-name {
  font-size: 1.5rem;
  font-weight: bold;
}

/* Enlaces del navbar */
.nav-links {
  display: flex;
  gap: 20px;
}

.nav-links a {
  color: rgb(2, 2, 2);
  font-weight: bold;
  text-decoration: none;
  font-size: 1rem;
}

/* Estilo para el enlace activo */
.nav-links a.router-link-exact-active {
  text-decoration: underline;
}

/* Hover */
.nav-links a:hover {
  text-decoration: underline;
}
</style>