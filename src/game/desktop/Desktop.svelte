<script>
	import wallpaper from "../../assets/wallpaper.jpg";
	import Terminal from "../apps/Terminal.svelte";
	import AppLauncher from "./taskbar/AppLauncher.svelte";
	import Taskbar from "./taskbar/Taskbar.svelte";
</script>

<!-- The main desktop -->
<section style="background-image: url('{wallpaper}');">
	<AppLauncher />
	<Terminal />
	<Taskbar />
</section>

<!-- Styling -->
<style lang="scss">
	section {
		width: 100%;
		height: 100%;
		background-size: cover;
		background-position: center;
	}
</style>
