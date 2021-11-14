<script>
	export let todoItem;
	export let onDelete;
	export let key;
</script>

<div class="card list-item">
	<span>{todoItem}</span>
	<button class="delete-button" on:click={onDelete(key)}>Remove</button>
</div>

<style>
	.card {
		box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
		transition: 0.3s;
		border-radius: 12px;
		padding: 14px 20px;
	}
	.list-item {
		display: flex;
    justify-content: space-between;
		align-items: center;
	}
	.delete-button {
		color: tomato;
		background-color: white;
		border: none;
		border-radius: 4px;
		margin: 0;
		cursor: pointer;
	}
</style>
