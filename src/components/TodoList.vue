<template>
	<div id="todo-list">
		<TodoItem id="todo-item" :data="dataTest" />
	</div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
	name: 'TodoList',
	components: {
		TodoItem
	},
	data: () => {
		return {
			dataTest: {
				title: "Teste 2",
				completed: true
			}
		}
	}
}
</script>


<style scoped>
	#todo-item {
		margin: 2vw 3vw;
		flex: 1;
		display: flex;
		justify-content: center;
		align-items: center;
		width: 10vw;
		height: 5vw;
		background-color: rgb(181, 205, 250);
	}

	#todo-list {
		margin: 0px;
		padding: 0px;
		display: flex;
		background-color: hsl(0, 0%, 92%);
		flex-wrap: wrap;
	}
</style>
