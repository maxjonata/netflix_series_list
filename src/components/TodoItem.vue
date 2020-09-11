<template>
	<div :id="id">
		<p id="todo-item-title">{{data.title}}</p>
	</div>
</template>

<script>
export default {
	name: 'TodoItem',
	props: {
		id: String,
		data: Object,
	},
	data: ()=>{
		return {
			completed: this.props.data.completed,
			title: this.prop.data.title
		}
	}
}
</script>


<style scoped>
	#todo-item {
		user-select: none;
	}
</style>
