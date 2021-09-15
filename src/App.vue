<template>
  <Navbar />
        
  <div class="container">
    <main>
      <router-view/>
    </main>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>


<style lang="scss">
@import '~materialize-css/dist/css/materialize.min.css';

.container-lg {
  max-width: 1280px;
  margin: 0 auto;
}
</style>