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

<section class="flex flex-col space-y-4">
	{#each tasks as task}
		<article
			transition:fade
			class="flex items-center justify-between rounded-md bg-white/5 px-4 py-4"
		>
			<label class="capitalize">
				<input class="mr-2" type="checkbox" checked={task.done} onchange={() => toggleDone(task)} />
				{task.title}
			</label>
			<button
				class="rounded border border-blue-500 px-4 py-2 text-blue-500"
				onclick={() => removeTask(task.id)}>Remove</button
			>
		</article>
	{/each}
</section>
