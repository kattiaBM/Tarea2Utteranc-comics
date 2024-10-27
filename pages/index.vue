<template>
  <div class="container">
    <h1>Bienvenido al Catálogo de Cómics</h1>
    <p>Explora los diferentes cómics, personajes e ilustradores.</p>
    <ul>
      <li>
        <NuxtLink to="/comics">Ver Cómics</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/personajes">Ver Personajes</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/ilustradores">Ver Ilustradores</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  head () {
    return {
      title: 'Catálogo de Cómics - Inicio'
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Asegura que el contenedor cubra toda la pantalla */
  width: 100%; /* Cambiado a 100% para que se ajuste al ancho de la pantalla */
  background-image: url('/image/Portada comics.jpg');
  background-size: cover; /* La imagen cubrirá todo el contenedor */
  background-position: center;
  background-repeat: no-repeat; /* Evita que la imagen se repita */
  color: #2cc4af;
  text-align: center;
  padding: 0;
}

h1 {
  font-size: 4em;
  color: #2fcbf1;
}

p {
  font-size: 1.5em;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 10px 0;
}

a {
  color: #3478b1;
  text-decoration: none;
  font-size: 2.2em;
}

a:hover {
  text-decoration: underline;
}
</style>
