<script lang="ts" context="module">
	let windows = new Map<number, unknown>();

	function nextWindowId(): number {
		let windowId = 0;
		while (windows.has(windowId)) windowId++;
		return windowId;
	}
</script>

<script lang="ts">
	import { onMount } from "svelte";

	/** The title that gets displayed on the upper left of the window.*/
	export let name: string;

	/** The window element. */
	let window: HTMLElement;

	/**
	 * The unique window ID associated with this window. Every window gets a unique ID upon creation. This is used to
	 * identify the window for things like closing it.
	 */
	export const id: number = nextWindowId();

	/** Makes a window "draggable". This is called when the component is mounted onto the DOM. */
	function makeDraggable(element: HTMLElement) {
		let pos1 = 0;
		let pos2 = 0;
		let pos3 = 0;
		let pos4 = 0;

		/**
		 * Whether the mouse is currently held down on the titlebar of this component. We can't actually listen for a
		 * "click-and-drag" directly; Instead, we listen for the mouse being pressed down on the titlebar, we remember
		 * whether it's pressed (by storing it here), and then we listen for any mouse movement, and IF it's pressed
		 * on the titlebar, we drag the window around.
		 */
		let mouseIsPressedOnTitlebar = false;

		/** The titlebar of the window. This is the initial <div> placed at the top of the window. */
		let titlebar = element.firstElementChild! as HTMLDivElement;

		/** Listen for mouse clicks on the titlebar, as explained above. */
		titlebar.addEventListener("mousedown", (event) => {
			mouseIsPressedOnTitlebar = true;
			event.preventDefault();
			pos3 = event.clientX;
			pos4 = event.clientY;
		});

		/** Listen for un-mouse clicks on the titlebar, as explained above. */
		titlebar.addEventListener("mouseup", () => {
			mouseIsPressedOnTitlebar = false;
		});

		/** Listen for any mouse movement on the whole document, as explained above. */
		document.addEventListener("mousemove", (event) => {
			if (mouseIsPressedOnTitlebar) {
				event.preventDefault();
				pos1 = pos3 - event.clientX;
				pos2 = pos4 - event.clientY;
				pos3 = event.clientX;
				pos4 = event.clientY;
				element.style.top = element.offsetTop - pos2 + "px";
				element.style.left = element.offsetLeft - pos1 + "px";
			}
		});
	}

	onMount(() => {
		makeDraggable(window);
	});
</script>

<!-- Main window content -->
<section bind:this={window}>
	<!-- Titlebar -->
	<div>
		<!-- App label -->
		<button>{name}</button>
		<button></button>
		<!-- Close button -->
		<button></button>
	</div>

	<!-- Inner window content -->
	<slot />
</section>

<style lang="scss">
	// Window
	section {
		width: 800px;
		height: 600px;
		background-color: lightgray;
		padding: 0.5rem;
		position: absolute;
		top: 100px;
		left: 100px;
		border-top: 4px solid ghostwhite;
		border-left: 4px solid ghostwhite;
		border-right: 4px solid gray;
		border-bottom: 4px solid gray;

		// Titlebar
		div {
			width: calc(100% + 8px);
			height: 2rem;
			background: red;
			position: absolute;
			left: -4px;
			top: calc(-2rem + -4px);
			background-color: lightgray;
			border-top: 4px solid ghostwhite;
			border-left: 4px solid ghostwhite;
			border-right: 4px solid gray;
			border-bottom: 4px solid gray;
			cursor: url("/src/assets/icons/cursor_move.png"), auto;
			display: flex;
			padding: 5px;
			gap: 0.5rem;
			font-family: "Courier New";

			// Close & Minimize Buttons
			button {
				border-top: 3px solid ghostwhite;
				border-left: 3px solid ghostwhite;
				border-right: 3px solid gray;
				border-bottom: 3px solid gray;

				// App name label
				&:first-child {
					margin-right: auto;
				}
			}
		}
	}
</style>
