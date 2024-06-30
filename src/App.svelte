<script>
	import { onMount } from "svelte";
	import Bar from "./bar.svelte";

	export let timeArr;
	let showSec = localStorage.getItem("showSec") == "true" || false;

	timeArr = getTime().split(":");
	let timer;

	onMount(() => {
		timer = setInterval(() => {
			timeArr = getTime().split(":");
		}, 1000);
	});

	function getTime() {
		let timestamp = Date.now();
		timestamp = Number(timestamp);
		const date = new Date(timestamp);

		const hours = ("0" + date.getHours()).slice(-2);
		const minutes = ("0" + date.getMinutes()).slice(-2);
		const seconds = ("0" + date.getSeconds()).slice(-2);

		if (showSec) {
			return `${hours}:${minutes}:${seconds}`;
		}
		return `${hours}:${minutes}`;
	}

	function toggle() {
		showSec = !showSec;
		timeArr = getTime().split(":");
		localStorage.setItem("showSec", showSec);
	}
</script>

<main>
	<div class="timeContainer" on:click={toggle}>
		<h1>
			{#each timeArr as str, i}
				<span>{str}</span>
				{#if i < timeArr.length - 1}
					<span class="spliter">:</span>
				{/if}
			{/each}
		</h1>
	</div>
	<Bar></Bar>
</main>

<style>
	main {
		text-align: center;
		width: 90vw;
		box-sizing: border-box;
		max-width: 768px;
		margin: auto;
	}

	.timeContainer {
		background-color: #f4f4f4;
		border-radius: 1rem;
		padding: 1rem;
		user-select: none;
		container-type: inline-size;
		cursor: pointer;
	}

	h1 {
		font-size: 4rem;
		font-weight: 200;
		font-family:
			system-ui,
			-apple-system,
			BlinkMacSystemFont,
			"Segoe UI",
			Roboto,
			Oxygen,
			Ubuntu,
			Cantarell,
			"Open Sans",
			"Helvetica Neue",
			sans-serif;
		display: flex;
		justify-content: center;
	}

	@keyframes fading {
		from {
			opacity: 1;
		}
		to {
			opacity: 0.5;
		}
	}

	.spliter {
		animation-name: fading;
		animation-duration: 0.735s;
		animation-timing-function: linear;
		animation-iteration-count: infinite;
		animation-direction: alternate-reverse;
	}

	@media (max-width: 900px) {
		h1 {
			font-size: 8rem;
		}
	}

	@media (max-width: 640px) {
		h1 {
			font-size: 6rem;
			font-size: 15cqw;
		}
	}

	@media (min-width: 900px) {
		h1 {
			font-size: 10rem;
		}
	}

	@media (prefers-color-scheme: dark) {
		.timeContainer {
			background-color: #141414;
			color: #fff;
		}
	}
</style>
