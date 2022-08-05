<script>
	import { consoleContent } from '../stores/console.js';
</script>

<main
	class="h-7 w-full border-t bg-panelBgLight border-uiLineLight dark:(bg-panelBgDark border-uiLineDark)"
>
	<div class="bg-red-400 h-80 w-full absolute">{$consoleContent}</div>
</main>
