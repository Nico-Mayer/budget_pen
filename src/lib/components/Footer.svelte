<script>
	import { consoleOpen } from '../stores/console.js';
</script>

<main
	class="h-7 w-full border-t bg-panelBgLight border-uiLineLight dark:(bg-panelBgDark border-uiLineDark) text-xs flex items-center px-2 z-10"
>
	<button
		class="flex items-center bg-panelFgDark rounded-full px-1"
		on:click={() => ($consoleOpen = !$consoleOpen)}
	>
		<div class="i-mdi-console-line mr-1" />
		console</button
	>
</main>
