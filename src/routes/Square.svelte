<script lang="ts">
	import { getTwemojiURL } from "./utils";
	import { send } from "./transitions";

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
	export let group: "a" | "b";
</script>

<div class="square" class:flipped={selected || found}>
	<button on:click />

	<div class="background"></div>

	{#if !found}
		<img
			out:send={{ key: `${emoji}:${group}` }}
			alt={emoji}
			src={getTwemojiURL(emoji)}
		/>
	{/if}
</div>

<style>
	.square {
		display: flex;
		justify-content: center;
		align-items: center;
		transform-style: preserve-3d;
		transition: transform 0.4s;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		backface-visibility: hidden;
		background: #eee;
		border: 0;
		border-radius: 1em;
		font-size: inherit;
	}

	.background {
		position: absolute;
		background: white;
		transform: rotateY(180deg);
		backface-visibility: hidden;
		width: 100%;
		height: 100%;
		border: 0.5em solid #eee;
		border-radius: 1em;
	}

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
		transform: rotateY(180deg);
		backface-visibility: hidden;
	}
</style>
