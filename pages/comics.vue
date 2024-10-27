<template>
  <div>
    <h1>Catálogo de Cómics</h1>
    <ul>
      <li v-for="comic in comics" :key="comic.id" class="comic-item">
        <!-- Mostrar la portada del cómic centrada -->
        <img :src="comic.portada" :alt="comic.titulo" class="comic-image">

        <h2>{{ comic.titulo }}</h2>
        <p><strong>Editorial:</strong> {{ comic.editorial }}</p>

        <!-- Iterar sobre personajes y mostrar enlaces -->
        <p><strong>Personajes:</strong></p>
        <ul class="character-list">
          <li v-for="personajeId in comic.personajes" :key="personajeId">
            <router-link :to="`/personajes/${personajeId}`" class="link">
              Ver Personaje {{ personajeId }}
            </router-link>
          </li>
        </ul>

        <!-- Iterar sobre ilustradores y mostrar enlaces -->
        <p><strong>Ilustradores:</strong></p>
        <ul class="illustrator-list">
          <li v-for="ilustradorId in comic.ilustradores" :key="ilustradorId">
            <router-link :to="`/ilustradores/${ilustradorId}`" class="link">
              Ver Ilustrador {{ ilustradorId }}
            </router-link>
          </li>
        </ul>
      </li>
    </ul>

    <!-- Botón para regresar al Home -->
    <div class="back-home">
      <NuxtLink to="/">
        <button>Regresar</button>
      </NuxtLink>
    </div>

    <!-- Sección de comentarios -->
    <div ref="comments"></div>
  </div>
</template>

<script>
export default {
  async asyncData () {
    try {
      // Cargar los datos desde el archivo estático comics.json
      const comics = await fetch('/data/comics.json').then(res => res.json())
      return { comics }
    } catch (error) {
      console.error('Error al cargar los cómics:', error)
      return { comics: [] }
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
/* Estilo del catálogo de cómics */
ul {
  list-style: none;
  padding: 0;
}

.comic-item {
  margin: 20px 0;
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 5px;
  background-color: #f9f9f9;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.comic-image {
  width: 80%; /* Ajusta el tamaño según sea necesario */
  max-width: 300px;
  height: auto;
  margin-bottom: 10px;
  object-fit: contain;
}

h2, p {
  color: black;
}

.back-home {
  margin-top: 20px;
}

.back-home button {
  background-color: #007bff;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.back-home button:hover {
  background-color: #0056b3;
}

.character-list, .illustrator-list {
  padding: 0;
  margin: 0;
  list-style: none;
}

.link {
  color: red;
  text-decoration: none;
}

.link:hover {
  text-decoration: underline;
}
</style>
