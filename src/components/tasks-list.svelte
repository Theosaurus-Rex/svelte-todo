<script lang="ts">
	import type { Task } from '../types';
	let { tasks, toggleDone }: { tasks: Task[]; toggleDone: (task: Task) => void } = $props();
</script>

<article>
	{#each tasks as task}
		<label>
			<input type="checkbox" checked={task.done} onchange={() => toggleDone(task)} />
			{task.title}
		</label>
	{/each}
</article>
