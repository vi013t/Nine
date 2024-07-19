<script lang="ts">
	import { onMount } from "svelte";

	const apps = ["settings", "chat", "files", "terminal", "draw", "calculator"];

	let appLauncher: HTMLElement;
	let visible = true;

	onMount(() => {
		document.addEventListener("keydown", (event) => {
			if (event.altKey) {
				if (visible) {
					slideDown(0);
					visible = false;
				} else {
					slideUp(600);
					visible = true;
				}
			}
		});
	});

	function slideDown(position: number) {
		appLauncher.style.transform = `translate(-50%, ${position}px)`;
		if (position < 600) {
			setTimeout(() => {
				slideDown(position + 20);
			}, 1);
		}
	}

	function slideUp(position: number) {
		appLauncher.style.transform = `translate(-50%, ${position}px)`;
		if (position > 0) {
			setTimeout(() => {
				slideUp(position - 20);
			}, 1);
		}
	}
</script>

<!-- Main app launcher content -->
<section bind:this={appLauncher}>
	{#each apps as app}
		<button>
			<img alt="{app} app icon" src="/src/assets/icons/{app}.png" />
		</button>
	{/each}
</section>

<!-- Styling -->
<style lang="scss">
	// Main app launcher
	section {
		display: flex;
		flex-wrap: wrap;
		background-image: linear-gradient(#333333, #222222);
		width: 25%;
		height: 50%;
		bottom: 6%;
		border-radius: 0.5rem;
		position: absolute;
		left: 50%;
		transform: translate(-50%, 0px);

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
