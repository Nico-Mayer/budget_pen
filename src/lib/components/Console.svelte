<script>
	import { consoleContent } from '../stores/console.js';
	import { consoleOpen } from '../stores/console.js';
	import { slide } from 'svelte/transition';
	import { resizing } from '../stores/store.js';

	function handleResize() {
		let consoleContainer = document.getElementById('consoleContainer');
		$resizing = true;
		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('mouseup', handleMouseUp);

		function handleMouseMove(e) {
			if (
				window.innerHeight - e.clientY > 100 &&
				window.innerHeight - e.clientY < window.innerHeight - 100
			) {
				consoleContainer.style.height = window.innerHeight - e.clientY + 'px';
				document.body.style.cursor = 'row-resize';
			}
		}

		function handleMouseUp() {
			$resizing = false;
			document.body.style.cursor = 'auto';
			window.removeEventListener('mousemove', handleMouseMove);
			window.removeEventListener('mouseup', handleMouseUp);
		}
	}
</script>

{#key $consoleOpen}
	<main
		class="bg-panelBgLight dark:bg-panelBgDark h-40 flex-col hidden w-full absolute bottom-0"
		id="consoleContainer"
		class:flex={$consoleOpen}
		transition:slide
	>
		<div
			class="px-2 py-3 bg-editorBgLight dark:bg-editorBgDark flex items-center cursor-row-resize"
			on:mousedown={handleResize}
		>
			<div class="i-mdi-console-line mr-1 text-xl" />
			<span>console:</span>
		</div>
		<section class="flex flex-col-reverse overflow-y-scroll">
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
