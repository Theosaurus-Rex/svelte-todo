<script lang="ts">
	import type { Task } from '../types';
	let {
		tasks,
		toggleDone,
		removeTask
	}: { tasks: Task[]; toggleDone: (task: Task) => void; removeTask: (index: number) => void } =
		$props();
</script>

<section>
	{#each tasks as task, index}
		<article>
			<label>
				<input type="checkbox" checked={task.done} onchange={() => toggleDone(task)} />
				{task.title}
			</label>
			<button onclick={() => removeTask(index)}>Remove</button>
		</article>
	{/each}
</section>
