<script lang="ts">
	import alarmSound from "../../assets/sounds/alarm.wav";
	import typewriterSound from "../../assets/sounds/typewriter.wav";

	/**
	 * The dialogue lines. These are lines that appear one after the other on the screen, and the dialogue is progressed when
	 * the user presses spacebar.
	 */
	const lines = [
		"wake up.",
		"5:00 AM",
		"where am i?",
		"who... am i?",
		"i cant remember anything.",
		"its dark. im scared.",
		"theres nothing here but a mattress and a computer.",
		"...",
		"the door is locked.",
		"...",
		"i guess all i can do is check the computer.",
	];

	/**
	 * The color of the text being displayed. This is "white", except for the alarm clock time, which is displayed in "red".
	 */
	let color = "white";

	/**
	 * The index of the current line being displayed on the screen. This is updated when the user presses spacebar to progress
	 * the dialogue.
	 */
	let currentLineIndex = 0;

	/**
	 * The current text on the screen. This is animated through the `refreshCurrentText` function, which updates the current text
	 * character by character when the dialogue progresses.
	 */
	let currentText = lines[currentLineIndex];

	/**
	 * The main intro element, which contains the dialogue text.
	 */
	let intro: HTMLElement;

	/**
	 * The alarm audio, which is played when the alarm clock screen appears. The audio is stopped when the next dialogue is played.
	 */
	let alarmAudio = new Audio(alarmSound);

	/**
	 * Whether or not the current typewriter animation is done. Each line of dialogue is added to the screen slowly with a typewriter-style
	 * animation. If this variable is set to false, that means that there is currently an ongoing animation. This is used to throttle user input;
	 * i.e., the user should not be able to press the spacebar while an animation is in progress.
	 */
	let isAnimationDone = true;

	// Listen for spacebar presses
	document.addEventListener("keypress", (event) => {
		// Typing animation is still in progress - don't allow input
		if (!isAnimationDone) {
			return;
		}

		// Spacebar pressed
		if (event.key === " ") {
			// Last line - end the intro
			if (currentLineIndex >= lines.length - 1) {
				intro.remove();
			}

			// Not last line - display the next one
			else {
				currentLineIndex++;
				currentText = "";
				isAnimationDone = false;
				refreshCurrentText();
				if (currentLineIndex === 1) {
					alarmAudio.play();
					color = "red";
				} else if (currentLineIndex == 2) {
					alarmAudio.pause();
					color = "white";
				}
			}
		}
	});

	/**
	 * Refreshes the text that's being displayed on the screen. This should be called whenever the used advances to a new line of dialogue, and
	 * `currentText` is updated. This recursively calls itself to add one character of the dialogue to the line every 65ms. When the animation is
	 * complete and there is no more text to display, the `isAnimationDone` variable will be set to `true`. Note that this will return after the
	 * first character is added, not when the entire animation is done, so `isAnimationDone` should be used as the correct way to check if the
	 * animation is complete
	 *
	 * @param index The index of the dialogue line to add to the current text.
	 */
	function refreshCurrentText(index: number = 0) {
		currentText += lines[currentLineIndex][index];
		new Audio(typewriterSound).play();
		if (index < lines[currentLineIndex].length - 1) {
			setTimeout(() => {
				refreshCurrentText(index + 1);
			}, 65);
		} else {
			isAnimationDone = true;
		}
	}
</script>

<!-- Main content -->
<section bind:this={intro} style:color>
	{currentText}
</section>

<!-- Styling -->
<style lang="scss">
	// Main content area
	section {
		// Cover the whole screen
		position: absolute;
		top: 0px;
		left: 0px;
		width: 100%;
		height: 100%;

		// Center the text
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		padding: 3rem;

		// Black background; color is set dynamically
		background-color: black;

		// Big typewriter text
		font-family: "Special Elite";
		font-size: 7rem;
	}
</style>
