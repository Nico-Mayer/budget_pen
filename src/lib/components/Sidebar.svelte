<script>
	import Editor from './Editor.svelte';
	import { Pane, Splitpanes } from 'svelte-splitpanes';
	import { resizing, html, css, js } from '../stores/store.js';
	import { onMount } from 'svelte';

	let sidebar;

	function handleSidebarResize() {
		$resizing = true;
		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('mouseup', handleMouseUp);

		function handleMouseMove(e) {
			if (e.clientX > 300) {
				sidebar.style.width = e.clientX + 'px';
				document.body.style.cursor = 'col-resize';
			}
		}
		function handleMouseUp() {
			$resizing = false;
			document.body.style.cursor = 'auto';
			window.removeEventListener('mousemove', handleMouseMove);
			window.removeEventListener('mouseup', handleMouseUp);
		}
	}

	onMount(() => {
		let splitters = document.querySelectorAll('.splitpanes__splitter');

		for (let i = 0; i < splitters.length; i++) {
			switch (i) {
				case 0:
					splitters[i].classList.add('html-splitter');
					break;
				case 1:
					splitters[i].classList.add('js-splitter');
					break;
				case 2:
					splitters[i].classList.add('css-splitter');
					break;
			}
		}
	});
</script>

<section bind:this={sidebar} class="flex min-w-[380px] w-[472px]">
	<Splitpanes horizontal={true} theme="own" firstSplitter={true}>
		<Pane maxSize={100} class="html-pane">
			<Editor lang={'xml'} bind:value={$html} />
		</Pane>

		<Pane maxSize={100}>
			<Editor lang={'javascript'} bind:value={$js} />
		</Pane>

		<Pane maxSize={100}>
			<Editor lang={'css'} bind:value={$css} />
		</Pane>
	</Splitpanes>

	<div
		on:mousedown={handleSidebarResize}
		class="flex h-full w-[14px] cursor-col-resize border-x border-uiLineLight bg-panelBgLight dark:(border-uiLineDark bg-panelBgDark) items-center"
	>
		<div class="i-charm-menu-hamburger rotate-90 dark:text-fontDark text-fontLight" />
	</div>
</section>

<style>
	:global(.CodeMirror-gutters) {
		background: transparent;
		border: none;
	}
	:global(.splitpanes__splitter) {
		--at-apply: 'border-t border-uiLineLight dark:border-uiLineDark';
		--at-apply: 'bg-panelBgLight dark:bg-panelBgDark';
		height: 44px;
		position: relative;
		cursor: row-resize;
	}
	:global(.splitpanes__splitter:before) {
		--at-apply: 'bg-editorBgLight dark:bg-editorBgDark';
		--at-apply: 'border-t-3 dark:border-white/10 border-black/20';
		display: flex;
		align-items: center;
		padding-left: 50px;
		height: 100%;
		background-repeat: no-repeat;
		background-position: 15px 50%;
		background-size: 20px;
		width: 110px;
	}
	:global(.html-splitter) {
		cursor: auto;
		border: none;
	}
	:global(.html-splitter.splitpanes__splitter:before) {
		content: 'HTML';
		background-image: url('https://api.iconify.design/icomoon-free:html-five.svg?color=%23FF694B');
	}
	:global(.js-splitter.splitpanes__splitter:before) {
		content: 'JS';
		background-image: url('https://api.iconify.design/cib:javascript.svg?color=%23F7DD1E');
	}
	:global(.css-splitter.splitpanes__splitter:before) {
		content: 'CSS';
		background-image: url('https://api.iconify.design/icomoon-free:css3.svg?color=%2330ace0');
	}
</style>
