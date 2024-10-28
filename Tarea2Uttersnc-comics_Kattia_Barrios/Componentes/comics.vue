<template>
  <div>
    <h1>Comic: {{ comic.nombre }}</h1>
    <!-- Imagen dinámica del cómic -->
    <img :src="`/image/${comic.imagen}`" :alt="comic.nombre" >

    <!-- Ejemplo de imagen estática (comprueba la ubicación del archivo) -->
    <img src="/image/spider-man.jpg" alt="comic 1">

    <p>Personaje: {{ comic.personaje }}</p>
    <p>Descripcion: {{ comic.descripcion }}</p>
  </div>
</template>

<script>
export default {
  async asyncData ({ params }) {
    try {
      // Cargar datos de los cómics desde el archivo JSON
      const comics = await fetch('/data/comics.json').then(res => res.json())

      // Buscar el cómic por nombre usando el parámetro de la ruta
      const comic = comics.find(c => c.nombre === params.nombre)

      // Verificar si el cómic existe
      if (!comic) {
        throw new Error('Comic no encontrado')
      }

      return { comic }
    } catch (error) {
      console.error('Error al cargar el cómic:', error)
      return { comic: {} }
    }
  }
}
</script>

<style scoped>
/* Estilos opcionales */
img {
  max-width: 100%;
  height: auto;
  margin-bottom: 20px;
}
</style>
