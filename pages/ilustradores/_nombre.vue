<template>
  <div class="container">
    <!-- Botón para regresar al Home -->
    <button class="home-button" @click="goHome">Inicio</button>

    <h1>Ilustradores</h1>

    <!-- Enlaces a otras secciones -->
    <nav>
      <NuxtLink to="/comics" class="link">Comics</NuxtLink> |
      <NuxtLink to="/personajes" class="link">Personajes</NuxtLink>
    </nav>

    <!-- Lista de Ilustradores -->
    <ul class="ilustradores-list">
      <li v-for="ilustrador in ilustradores" :key="ilustrador.id" class="ilustrador-item">
        <img :src="ilustrador.image" :alt="ilustrador.nombre" class="ilustrador-image">
        <h2>{{ ilustrador.nombre }}</h2>
        <p>Estilo: {{ ilustrador.estilo }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData () {
    // Cargar los datos desde el archivo estático ilustrador.json
    try {
      const ilustradores = await fetch('/data/ilustradores.json').then(res => res.json())
      return { ilustradores }
    } catch (error) {
      console.error('Error al cargar los ilustradores:', error)
      return { ilustradores: [] }
    }
  },
  mounted () {
    // Crear y agregar el script de Utterances dinámicamente
    const script = document.createElement('script')
    script.src = 'https://utteranc.es/client.js'
    script.setAttribute('repo', 'KattiaBM/Tarea2Utteranc-comics')
    script.setAttribute('issue-term', 'pathname')
    script.setAttribute('theme', 'github-light')
    script.setAttribute('crossorigin', 'anonymous')
    script.async = true
    this.$refs.comments.appendChild(script)
  }
}
</script>

<style scoped>
/* Centrar el contenido */
.container {
  text-align: center;
  padding: 20px;
}

/* Estilo del botón Home */
.home-button {
  position: absolute;
  top: 20px;
  left: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.home-button:hover {
  background-color: #0056b3;
}

/* Enlaces de navegación */
nav {
  margin-bottom: 20px;
}

.link {
  color: #007bff;
  text-decoration: none;
  margin: 0 10px;
}

.link:hover {
  text-decoration: underline;
}

/* Estilo de la lista de ilustradores */
.ilustradores-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.ilustrador-item {
  margin-bottom: 10px;
  border: 1px solid #ddd;
  padding: 5px;
  border-radius: 5px;
  background-color: #f9f9f9;
  display: flex;
  flex-direction: initial;
  align-items: center;
  text-align: center;
}

.ilustrador-image {
  width: 80px; /* Ajusta el tamaño según sea necesario */
  height: auto;
  margin-bottom: 10px;
}

h2, p {
  color: black;
}
</style>
