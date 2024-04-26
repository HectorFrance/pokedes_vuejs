<script setup>
// importação  dos elementos vue-router
import { RouterLink, RouterView } from 'vue-router'

// importação bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'

//importar estilo css
import './assets/estilo.css'

// importar compenentes de navegação 
import BarraNavegacao from './components/BarraNAvegacao.vue'

</script>

<template>
  <!--Barra de navegação-->
  <BarraNavegacao></BarraNavegacao>

  <!-- Visualizar conteudo das pagians -->
  <RouterView />
</template>