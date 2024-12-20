<script lang="ts">
	import TasksForm from '../components/tasks-form.svelte';
	import TasksList from '../components/tasks-list.svelte';
	import type { Task } from '../types';
	let tasks = $state<Task[]>([]);
	let totalDone = $derived(tasks.reduce((total, task) => total + Number(task.done), 0));

	function addTask(newTask: string) {
		// This now triggers a re-render in svelte 5
		tasks.push({
			id: crypto.randomUUID(),
			title: newTask,
			done: false
		});
	}

	function toggleDone(task: Task) {
		task.done = !task.done;
	}
</script>

<main>
	<h1>Tasks App</h1>
	<TasksForm {addTask} />
	<p>{totalDone} / {tasks.length} tasks completed</p>
	<TasksList {tasks} {toggleDone} />
</main>
