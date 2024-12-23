<template>  
  <NavBarComponent/>
  <router-view/>
</template>
<script>
import NavBarComponent from '@/components/navBarComponent.vue';

export default {
  components: {
    NavBarComponent
  }
}
</script>