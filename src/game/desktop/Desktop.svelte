<script>
	import Terminal from "../apps/Terminal.svelte";
	import AppLauncher from "./taskbar/AppLauncher.svelte";
	import Taskbar from "./taskbar/Taskbar.svelte";
</script>

<!-- The main desktop -->
<section>
	<AppLauncher />
	<Terminal />
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
