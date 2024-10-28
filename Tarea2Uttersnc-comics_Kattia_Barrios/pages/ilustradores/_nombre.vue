<template>
  <div class="ilustradores-page">
    <!-- Botón para regresar al Home -->
    <button class="btn-home" @click="goHome">Inicio</button>

    <h1>Ilustradores</h1>

    <!-- Enlaces a otras secciones -->
    <nav class="nav-links">
      <NuxtLink to="/comics" class="link">Comics</NuxtLink> |
      <NuxtLink to="/personajes" class="link">Personajes</NuxtLink>
    </nav>

    <!-- Lista de Ilustradores -->
    <ul class="ilustradores-list">
      <li v-for="ilustrador in ilustradores" :key="ilustrador.id" class="ilustrador-item">
        <img :src="ilustrador.image" :alt="ilustrador.nombre" class="ilustrador-image">
        <div class="ilustrador-info">
          <h2>{{ ilustrador.nombre }}</h2>
          <p>Estilo: {{ ilustrador.estilo }}</p>
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
    // Cargar los datos desde el archivo estático ilustradores.json
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
.ilustradores-page {
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

/* Estilo de la lista de ilustradores */
.ilustradores-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

/* Cada ítem de ilustrador */
.ilustrador-item {
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

.ilustrador-image {
  width: 100px; /* Ajusta el tamaño según sea necesario */
  height: auto;
  margin-bottom: 10px;
}

h2, p {
  color: black;
}
</style>
