<template>
  <div class="personajes-page">
    <!-- Botón para regresar al Home -->
    <button class="btn-home" @click="goHome">Inicio</button>

    <h1>Personajes</h1>

    <!-- Enlaces a otras secciones -->
    <nav class="nav-links">
      <NuxtLink to="/comics" class="link">Comics</NuxtLink> |
      <NuxtLink to="/ilustradores" class="link">Ilustradores</NuxtLink>
    </nav>

    <!-- Lista de Personajes -->
    <ul class="personajes-list">
      <li v-for="personaje in personajes" :key="personaje.id" class="personaje-item">
        <img :src="personaje.image" :alt="personaje.nombre" class="personaje-image">
        <div class="personaje-info">
          <h2>{{ personaje.nombre }}</h2>
          <p>Descripción: {{ personaje.descripcion }}</p>
        </div>
      </li>
    </ul>

    <!-- Sección de comentarios -->
    <div ref="comments"></div>
  </div>
</template>

<script>
export default {
  async asyncData () {
    // Cargar los datos desde el archivo estático personajes.json
    try {
      const personajes = await fetch('/data/personajes.json').then(res => res.json())
      return { personajes }
    } catch (error) {
      console.error('Error al cargar los personajes:', error)
      return { personajes: [] }
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
    this.$refs.comments.appendChild(script) // Usar refs para el div de comentarios
  },
  methods: {
    goHome () {
      this.$router.push('/') // Cambiar la ruta al home
    }
  }
}
</script>

<style scoped>
/* Contenedor principal de la página */
.personajes-page {
  text-align: center;
  padding: 20px;
}

/* Estilo del botón Home */
.btn-home {
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

.btn-home:hover {
  background-color: #0056b3;
}

/* Enlaces de navegación */
.nav-links {
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

/* Estilo de la lista de personajes */
.personajes-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

/* Cada ítem de personaje */
.personaje-item {
  margin: 20px;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 5px;
  background-color: #f9f9f9;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.personaje-image {
  width: 100px; /* Ajusta el tamaño según sea necesario */
  height: auto;
  margin-bottom: 10px;
}

h2, p {
  color: black;
}
</style>
