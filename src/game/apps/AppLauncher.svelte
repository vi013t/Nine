<script lang="ts">
	import Window from "./Window.svelte";

	const apps = ["settings", "chat", "files", "terminal", "draw", "calculator"];
</script>

<!-- Main app launcher content -->
<Window name="Apps">
	<div>
		{#each apps as app}
			<button>
				<img alt="{app} app icon" src="/src/assets/icons/{app}.png" />
			</button>
		{/each}
	</div>
</Window>

<!-- Styling -->
<style lang="scss">
	// Main app launcher
	div {
		display: flex;
		flex-wrap: wrap;

		// App button
		button {
			width: 5rem;
			height: 5rem;
			padding: 1rem;

			// App Image
			img {
				width: 100%;
				height: 100%;
				image-rendering: pixelated;
				image-rendering: -moz-crisp-edges;
				image-rendering: crisp-edges;
			}
		}
	}
</style>
