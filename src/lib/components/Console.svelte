<script>
	import { consoleContent } from '../stores/console.js';
	import { consoleOpen } from '../stores/console.js';
	import { slide } from 'svelte/transition';
</script>

{#key $consoleOpen}
	<main
		class="bg-panelBgLight dark:bg-panelBgDark w-full h-40 absolute bottom-6 flex-col hidden"
		class:flex={$consoleOpen}
		transition:slide
	>
		<div class="px-2 py-3 bg-editorBgLight dark:bg-editorBgDark flex items-center">
			<div class="i-mdi-console-line mr-1 text-xl" />
			<span>console:</span>
		</div>
		<section class="flex flex-col-reverse overflow-scroll">
			<div>
				{#each $consoleContent as log, i}
					<p
						class="px-2 py-1"
						class:dark:bg-editorBgDark={i % 2 !== 0}
						class:bg-editorBgLight={i % 2 !== 0}
					>
						{i}: {log}
					</p>
				{/each}
			</div>
		</section>
	</main>
{/key}
