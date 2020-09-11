<template>
  <div id="app">
	<div id="flexitem1">
		<NavBar />
	</div>
	<div id="flexitem2">
		<router-view/>
	</div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue'

export default {
	name: 'App',
	components: {
		NavBar
	}
}
</script>

<style>

body, html {
	margin: 0px;
	height: 100%;
}

#flexitem2 {
	flex: 1;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 100%;
  max-height: 100%;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
