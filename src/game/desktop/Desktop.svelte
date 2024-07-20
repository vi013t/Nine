<script lang="ts" context="module">
	import Taskbar from "./taskbar/Taskbar.svelte";

	export type Component = { new (properties: { target: HTMLElement }): unknown };

	let windows = new Set<unknown>();

	export function openWindow(component: Component) {
		new component({
			target: document.getElementById("desktop")!,
		});
	}
</script>

<!-- The main desktop -->
<section id="desktop">
	<Taskbar />
</section>

<!-- Styling -->
<style lang="scss">
	section {
		width: 100%;
		height: 100%;
		background-color: steelblue;
	}
</style>
