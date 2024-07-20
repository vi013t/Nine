<script lang="ts">
	import Window from "./Window.svelte";

	let terminal: HTMLElement;

	type Command = (positionalArguments: string[], shortArguments: string[], longArguments: string[]) => string;

	const commands = {
		echo(positionalArguments, shortArguments, longArguments) {
			return positionalArguments[0] + "<br/>";
		},
	} as const satisfies { [key: string]: Command };

	let currentCommand = "";

	document.addEventListener("keypress", (event) => {
		if (event.key === "Enter") {
			terminal.innerHTML += "<br/>";
			runCommand();
			terminal.innerHTML += "&gt; ";
			currentCommand = "";
			return;
		}
		terminal.innerHTML += event.key;
		currentCommand += event.key;
	});

	function runCommand() {
		const tokenTypes = {
			string: /^"[^"]*"/,
			longArgument: /^--\S+/,
			shortArgument: /^-\S+/,
			identifier: /^\S+/,
			whitespace: /^[\s\n\t\r ]+/,
		} as const satisfies { [key: string]: RegExp };

		type TokenType = keyof typeof tokenTypes;

		type Token = {
			type: TokenType;
			value: string;
		};

		function tokenize(code: string): Token[] {
			let remainingCode = code;
			let tokens: Token[] = [];
			let matchFound = false;
			while (remainingCode != "") {
				for (let tokenType of Object.keys(tokenTypes)) {
					let match = tokenTypes[tokenType as TokenType].exec(remainingCode);
					if (match) {
						tokens.push({
							type: tokenType as TokenType,
							value: match[0],
						});
						remainingCode = remainingCode.substring(match[0].length);
						matchFound = true;
						break;
					}
				}

				if (!matchFound) {
					throw `Unrecognized token: ${remainingCode}`;
				}
			}

			return tokens;
		}

		let tokens = tokenize(currentCommand);
		let longArguments = tokens.filter((token) => token.type === "longArgument").map((token) => token.value);
		let shortArguments = tokens.filter((token) => token.type === "shortArgument").map((token) => token.value);
		let command = tokens.shift()!.value;
		let positionalArguments = tokens.filter((token) => token.type === "identifier").map((token) => token.value);

		let commandToRun = commands[command as keyof typeof commands];
		if (!commandToRun) {
			terminal.innerHTML += `Unrecognized command: ${command}<br/>`;
			return;
		}

		let output = commands[command as keyof typeof commands](positionalArguments, shortArguments, longArguments);
		terminal.innerHTML += output;
	}
</script>

<Window name="Terminal">
	<p bind:this={terminal}>&gt;</p>
</Window>

<style lang="scss">
	p {
		font-family: "Courier New";
	}
</style>
