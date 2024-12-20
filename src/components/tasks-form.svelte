<script lang="ts">
	let newTask = $state('');
	let {
		addTask
	}: {
		addTask: (newTask: string) => void;
	} = $props();

	function formSubmitted(e: SubmitEvent) {
		e.preventDefault();
		addTask(newTask);
		newTask = '';
	}
</script>

<form onsubmit={formSubmitted}>
	<label
		>Task
		<input type="text" name="newTask" bind:value={newTask} />
	</label>
	<button>Add</button>
</form>
