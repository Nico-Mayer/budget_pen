<script>
	// @ts-nocheck
	import { isDark } from '../stores/darkMode';
	import 'codemirror/lib/codemirror.css';
	import 'codemirror/theme/ayu-mirage.css';
	import 'codemirror/theme/eclipse.css';
	import 'codemirror/mode/javascript/javascript';
	import 'codemirror/mode/css/css';
	import 'codemirror/mode/xml/xml';
	// ADDONS
	import 'codemirror/addon/fold/xml-fold.js';
	import 'codemirror/addon/edit/closetag.js';
	import 'codemirror/addon/edit/closebrackets.js';
	import CodeMirror from 'codemirror';
	import { onMount } from 'svelte';

	export let value;
	export let lang;
	let editor;
	let firstLoad = true;

	let theme;

	$: if ($isDark) {
		theme = 'ayu-mirage';
		if (!firstLoad) {
			editor.setOption('theme', 'ayu-mirage');
		}
	} else {
		theme = 'eclipse';
		if (!firstLoad) {
			editor.setOption('theme', 'eclipse');
		}
	}

	let textArea;

	onMount(() => {
		editor = CodeMirror.fromTextArea(textArea, {
			lineWrapping: true,
			mode: lang,
			smartIndent: true,
			lineNumbers: true,
			theme: theme,
			scrollbarStyle: 'null',
			autoCloseTags: true,
			autoCloseBrackets: {
				pairs: '()[]{}\'\'""',
				explode: '()[]{}\'\'""><'
			}
		});
		editor.focus();
		editor.on('change', () => {
			value = editor.getValue();
		});
		firstLoad = false;
		return () => {
			editor.toTextArea();
		};
	});
</script>

<div class="editor-container">
	<textarea bind:this={textArea} bind:value readonly />
</div>

<style>
	.editor-container {
		display: flex;
		flex-direction: column;
		flex-grow: 1;
		width: 100%;
		height: 100%;
	}
</style>
