<script lang="ts" context="module">
</script>

<script lang="ts">
	import Window from "./Window.svelte";

	type FileSystem = {
		cwd: string;
		root: Directory;
	};

	const fileSystem: FileSystem = {
		cwd: "/home/name",
		root: {
			name: "/",
			contents: [
				{
					name: "home",
					contents: [
						{
							name: "name",
							contents: [],
						},
					],
				},
			],
		},
	};

	type File = {
		name: string;
		contents: string;
	};

	type Directory = {
		name: string;
		contents: Entry[];
	};

	type Entry = File | Directory;
</script>

<Window name="Files" />
