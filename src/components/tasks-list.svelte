<script lang="ts">
	import { fade } from 'svelte/transition';
	import type { Task } from '../types';
	let {
		tasks,
		toggleDone,
		removeTask
	}: { tasks: Task[]; toggleDone: (task: Task) => void; removeTask: (id: string) => void } =
		$props();
</script>

<section>
	{#each tasks as task}
		<article transition:fade>
			<label>
				<input type="checkbox" checked={task.done} onchange={() => toggleDone(task)} />
				{task.title}
			</label>
			<button onclick={() => removeTask(task.id)}>Remove</button>
		</article>
	{/each}
</section>
