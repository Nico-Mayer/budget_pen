<script>
	import { consoleContent } from '../stores/console.js';
</script>

<main
	class="bg-panelBgLight dark:bg-panelBgDark w-full h-20 border-red-400 border absolute bottom-6 flex flex-col overflow-scroll hidden"
>
	{#each $consoleContent as log}
		<p>{log}</p>
	{/each}
</main>
