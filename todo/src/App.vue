<template>
  <div class="container">
    <div class="border p-4 mt-5">
      <router-view></router-view>
        <Footer />
    </div>
  </div>
</template>

<script>
import Footer from './components/Footer.vue';
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';
export default {
  name: 'App',
  components: {
    Footer
  },
}
</script>