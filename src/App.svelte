<script>
	import { isEmpty } from "lodash";
	import TodoItem from "./components/TodoItem.svelte";

	let currentItem = '';
	const preList = JSON.parse(localStorage.getItem('svelte-todo-list'));
	let todoList = isEmpty(preList) ? [] : preList;
	function addToList(e){
		e.preventDefault();
		if(!isEmpty(currentItem)) {
			todoList = [currentItem, ...todoList];
			currentItem = '';
			localStorage.setItem("svelte-todo-list", JSON.stringify(todoList));
		}
	
	}
	function removeFromList(item){
		const updatedList = todoList.filter(i => { return i.toUpperCase() != item.toUpperCase()});
		todoList = [...updatedList];
		localStorage.setItem("svelte-todo-list", JSON.stringify(updatedList));
	}
	$: todoListRenderer = todoList;
	$: count = todoListRenderer.length;
</script>

<section class="app">
	<div class="todo-app">
		<div class="todo-wrapper card">
			<h1 class="app-heading">Todo App</h1>
			<form on:submit={addToList}>
				<input class="input-todo" type="text" bind:value={currentItem} placeholder="What do you want to do today ? " />
				<button class="input-button" on:click={addToList}>Submit</button>
			</form>
			<span class="helper-text">Total count : {count}</span>
			{#if isEmpty(todoList)}
			<div class="empty-wrapper">
				<img src="data:image/jpeg;base64,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" alt="no tasks for today" />
				<p>You have no todos today !!!</p>
			</div>
			{/if}
			<ul class="list-wrapper">
				{#each todoListRenderer as item}
					<li class="item test">
						<!-- {item}
						<button style="margin-left: 24px;" value={item} on:click={removeFromList(item)}>Remove</button> -->
						<TodoItem todoItem={item} key={item} onDelete={removeFromList}  />
					</li>
				{/each}
			</ul>
		</div>
	</div>
</section>


<style>
	.app{
		min-height: 100vh;
		background: #333333;  /* fallback for old browsers */
		background: -webkit-linear-gradient(to right, #dd1818, #333333);  /* Chrome 10-25, Safari 5.1-6 */
		background: linear-gradient(to right, #dd1818, #333333); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
	}
	.todo-app {
		padding: 24px;
		min-height: 60vh;
		display: flex;
	}
	.app-heading {
		color: black;
		text-align: center;
		font-size: 36px;
		font-weight: 300;
	}
	.todo-wrapper { 
		padding: 40px;
		margin: auto;
		color: black;
		background-color: white;
		min-height: 500px;
	}
	.input-todo {
		width: 80%;
		padding: 14px 20px;
		border-radius: 4px;
	}
	.input-button {
		margin-left: 10px;
		color: white;
		background-color: tomato;
		border-color: tomato;
		border-radius: 4px;
		min-width: 100px;
		cursor: pointer;
		padding: 14px 20px;
	}
	.helper-text {
		font-size: 12px;
	}
	.empty-wrapper {
		text-align: center;
		padding: 20px;
		font-size: 24px;
	}
	.list-wrapper {
		list-style-type: none;
		padding: 0;
		width: 80%;
		margin: auto;
		margin-top: 40px;
	}
	.item {
		margin-top: 20px;
	}
	.card {
		box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
		transition: 0.3s;
		width: 40%;
		border-radius: 12px;
	}
	.input-button:hover {
		box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
	}
</style>
