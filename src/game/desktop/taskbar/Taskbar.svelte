<script lang="ts">
	const buttons = ["apps", "browser", "chat", "files"] as const satisfies string[];
</script>

<!-- Main taskbar content -->
<section>
	{#each buttons as button}
		<button>
			<img src="/src/assets/icons/{button}.png" alt="{button} taskbar icon" />
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
		border-top: 0.4rem solid ghostwhite;
		gap: 0.2rem;

		// App icon buttons on the taskbar
		button {
			height: 90%;
			aspect-ratio: 1;
			padding: 0.8rem;
			position: relative;

			// App icon selection background
			&::before {
				content: "";
				width: 100%;
				height: 100%;
				background-color: rgba(255, 255, 255);
				border-radius: 10px;
				position: absolute;
				top: 0px;
				left: 0px;
				opacity: 0%;
				transition: opacity 0.1s;
			}

			// Selection background only visible on hover
			&:hover::before {
				opacity: 5%;
			}

			// App icon itself
			img {
				width: 100%;
				height: 100%;
				background-size: cover;
				background-position: center;

				// Scale pixel art properly
				image-rendering: pixelated;
				image-rendering: -moz-crisp-edges;
				image-rendering: crisp-edges;
			}
		}
	}
</style>
