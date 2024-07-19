<script lang="ts">
	import lockscreen from "../../assets/textures/lockscreen.jpg";
	import power from "../../assets/textures/power.png";
	import profile from "../../assets/textures/profile.png";

	let password: string;
	let login: HTMLElement;

	function checkPassword() {
		if (password != "password") {
			password = "";
			return;
		}

		login.remove();
	}
</script>

<!-- The main login screen content -->
<section bind:this={login} style="background-image: url({lockscreen})">
	<div>
		<img alt="Login profile" src={profile} />
		<p>Nine</p>
		<input type="password" placeholder="Password" bind:value={password} />
		<button class="enter" on:click={checkPassword}>Enter</button>
		<button class="power" style="background-image: url({power})"></button>
	</div>
</section>

<style lang="scss">
	section {
		background-position: center;
		background-size: cover;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: absolute;
		left: 0px;
		top: 0px;

		div {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			gap: 2rem;
			background: lightgray;
			padding: 3rem;
			border-top: 10px solid ghostwhite;
			border-left: 10px solid ghostwhite;
			border-bottom: 10px solid gray;
			border-right: 10px solid gray;

			p {
				font-size: 2rem;
				font-family: "Consolas";
			}
		}

		// Profile picture
		img {
			// Scale pixel art properly
			width: 10rem;
			height: 10rem;
			image-rendering: pixelated;
			image-rendering: -moz-crisp-edges;
			image-rendering: crisp-edges;
		}

		input {
			background-color: lightgray;
			font-size: 2rem;
			border-bottom: 5px solid ghostwhite;
			border-right: 5px solid ghostwhite;
			border-top: 5px solid gray;
			border-left: 5px solid gray;
			font-family: "Courier New";
			font-weight: bold;
		}

		.power {
			position: fixed;
			height: 5rem;
			width: 5rem;
			background-size: cover;
			right: 2rem;
			bottom: 2rem;
			image-rendering: pixelated;
			image-rendering: -moz-crisp-edges;
			image-rendering: crisp-edges;
		}

		.enter {
			border-top: 5px solid ghostwhite;
			border-left: 5px solid ghostwhite;
			border-bottom: 5px solid gray;
			border-right: 5px solid gray;
			font-family: "Consolas";
			font-size: 2rem;
			padding: 0.5rem;
			padding-left: 1rem;
			padding-right: 1rem;
		}

		input[type="password"]::-ms-reveal,
		input[type="password"]::-ms-clear {
			display: none;
		}
	}
</style>
