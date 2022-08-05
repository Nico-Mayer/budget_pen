<script>
	import { consoleContent } from '../stores/console.js';
	import { consoleOpen } from '../stores/console.js';
	import { slide } from 'svelte/transition';
</script>

{#key $consoleOpen}
	<main
		class="bg-panelBgLight dark:bg-panelBgDark w-full h-20 absolute bottom-6 flex-col overflow-scroll hidden"
		class:flex={$consoleOpen}
		transition:slide
	>
		{#each $consoleContent as log}
			<p>{log}</p>
		{/each}
	</main>
{/key}
