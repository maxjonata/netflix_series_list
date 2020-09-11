<template>
	<div id="nav">
		<router-link id="navScopes" to="/">Netflix Series List</router-link>
		<router-link id="navScopes" to="/tutorial">Como achar o CSV</router-link>
	</div>
</template>

<script>
	export default {
		name: 'NavBar'
	}
</script>


<style scoped>
	@import 'https://fonts.googleapis.com/icon?family=Material+Icons';

	#nav {
		display: flex;
		justify-content: center;
		background-color: #141414;
	}

	#navScopes {
		color: #7B7B7B;
		flex: 1;
		width: 10vw;
		user-select: none;
		text-decoration: none;
		display: flex;
		align-items: center;
		justify-content: center;	
		flex-direction: column;
	}

	#nav #navScopes:hover {
		color: #E0E0E0;
	}

	#nav #navScopes.router-link-exact-active {
		color: #E50914;
	}
</style>
