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

<form class="flex flex-col" onsubmit={formSubmitted}>
	<div class="mb-4 flex flex-col">
		<label for="newTask">Task</label>
		<input class="rounded-md bg-white/5" type="text" name="newTask" bind:value={newTask} />
	</div>

	<button class="w-fit place-self-end rounded-md bg-blue-500 px-4 py-2">Add</button>
</form>
