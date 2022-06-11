<template>
  <v-app class="bg-grey-lighten-4">
    <Navbar/>
    <v-main>
      <router-view/>
    </v-main>
    <div>
      <Footer/>
    </div>
  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Footer from '@/components/Footer.vue'
export default {
  name: 'App',
  components: { Navbar, Footer },
  data: () => ({
    //
  }),
}
</script>
