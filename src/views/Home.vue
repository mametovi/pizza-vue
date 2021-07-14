<template>
  <div class="home">

    <task />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import task from '../components/Task.vue'

export default {
  name: 'Home',
  components: {
    task
  }
}
</script>
