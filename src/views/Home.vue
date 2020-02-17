<template>
  <div class="home">
   <cookitem/>
  </div>
</template>

<script>
// @ is an alias to /src

import cookitem from '../components/cookitem'

export default {
  name: 'Home',
  components: {
    cookitem
  }
}
</script>
