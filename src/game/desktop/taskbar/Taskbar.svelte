<script lang="ts">
	const buttons = ["Apps", "Browser", "Chat", "Files"] as const satisfies string[];
</script>

<!-- Main taskbar content -->
<section>
	{#each buttons as button}
		<button>
			<img src="/src/assets/icons/{button.toLowerCase()}.png" alt="{button} taskbar icon" />
			{button}
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
				border-bottom: 5px solid ghostwhite;
				border-right: 5px solid ghostwhite;
				border-top: 5px solid gray;
				border-left: 5px solid gray;
			}
		}
	}
</style>
