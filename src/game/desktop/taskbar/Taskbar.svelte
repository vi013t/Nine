<script lang="ts">
	import AppLauncher from "../../apps/AppLauncher.svelte";
	import Browser from "../../apps/Browser.svelte";
	import Chat from "../../apps/Chat.svelte";
	import Files from "../../apps/Files.svelte";
	import { openWindow, type Component } from "../Desktop.svelte";

	const pinnedApps = [
		{ name: "Apps", app: AppLauncher },
		{ name: "Browser", app: Browser },
		{ name: "Chat", app: Chat },
		{ name: "Files", app: Files },
	] as const satisfies {
		name: string;
		app: Component;
	}[];
</script>

<!-- Main taskbar content -->
<section>
	{#each pinnedApps as app}
		<button on:click={() => openWindow(app.app)}>
			<img src="/src/assets/icons/{app.name.toLowerCase()}.png" alt="{app} app icon" />
			{app.name}
		</button>
	{/each}
</section>

<!-- Styling -->
<style lang="scss">
	// The main taskbar itself
	section {
		width: 100%;
		height: 4%;
		position: fixed;
		bottom: 0px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: lightgray;
		border-top: 0.2rem solid ghostwhite;
		gap: 0.4rem;

		// App icon buttons on the taskbar
		button {
			height: 80%;
			padding: 0.8rem;
			position: relative;
			font-family: "Consolas";
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 0.5rem;

			// Old-fashioned borders
			border-top: 3px solid ghostwhite;
			border-left: 3px solid ghostwhite;
			border-bottom: 3px solid gray;
			border-right: 3px solid gray;

			// App icon itself
			img {
				height: 1rem;
				width: 1rem;

				// Scale pixel art properly
				image-rendering: pixelated;
				image-rendering: -moz-crisp-edges;
				image-rendering: crisp-edges;
			}

			&:active {
				// Old-fashioned borders
				border-bottom: 3px solid ghostwhite;
				border-right: 3px solid ghostwhite;
				border-top: 3px solid gray;
				border-left: 3px solid gray;
			}
		}
	}
</style>
