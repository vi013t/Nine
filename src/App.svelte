<script lang="ts">
	import click from "./assets/sounds/click.wav";
	import clack from "./assets/sounds/typewriter.wav";
	import Desktop from "./game/desktop/Desktop.svelte";
	import Intro from "./game/intro/Intro.svelte";
	import LoginScreen from "./game/login/LoginScreen.svelte";

	document.addEventListener("click", (_event) => {
		new Audio(click).play();
	});

	document.addEventListener("keypress", (_event) => {
		new Audio(clack).play();
	});
</script>

<main>
	<Desktop />
	<LoginScreen />
	<Intro />
</main>

<style lang="scss">
	main {
		width: 100%;
		height: 100%;
	}
</style>
