<template>
  <div class="home">
	<DropAndList />
  </div>
</template>

<script>
// @ is an alias to /src
import DropAndList from '@/components/DropAndList.vue'

export default {
  name: 'Home',
  components: {
	DropAndList
  }
}
</script>

<style scoped>
	.home {
		height: 100%;
	}
</style>