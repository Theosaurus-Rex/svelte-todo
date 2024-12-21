<script lang="ts">
	import TasksForm from '../components/tasks-form.svelte';
	import TasksList from '../components/tasks-list.svelte';
	import type { Filter, Task } from '../types';

	let currentFilter = $state<Filter>('all');
	let tasks = $state<Task[]>([]);
	let totalDone = $derived(tasks.reduce((total, task) => total + Number(task.done), 0));

	let filteredTasks = $derived.by(() => {
		switch (currentFilter) {
			case 'all':
				return tasks;
			case 'done':
				return tasks.filter((task) => task.done);
			case 'todo':
				return tasks.filter((task) => !task.done);
		}
		return tasks;
	});

	function addTask(newTask: string) {
		tasks.push({
			id: crypto.randomUUID(),
			title: newTask,
			done: false
		});
	}

	function toggleDone(task: Task) {
		task.done = !task.done;
	}

	function removeTask(id: string) {
		const index = tasks.findIndex((task) => task.id === id);
		tasks.splice(index, 1);
	}
</script>

{#snippet filterButton(filter: Filter)}
	<button
		class="rounded border px-4 py-2 capitalize text-white"
		class:bg-white={currentFilter === filter}
		class:text-black={currentFilter === filter}
		onclick={() => (currentFilter = filter)}
	>
		{filter}
	</button>
{/snippet}

<main class="h-screen bg-neutral-800 p-4 text-white lg:px-80">
	<h1 class="my-2 text-3xl font-semibold">Tasks App</h1>
	<TasksForm {addTask} />
	<p>
		{#if tasks.length}
			{totalDone} / {tasks.length} tasks completed
		{:else}
			Add a task to get started.
		{/if}
	</p>
	{#if tasks.length}
		<div class="my-4 flex justify-end space-x-2">
			{@render filterButton('all')}
			{@render filterButton('done')}
			{@render filterButton('todo')}
		</div>
	{/if}
	<TasksList tasks={filteredTasks} {toggleDone} {removeTask} />
</main>
