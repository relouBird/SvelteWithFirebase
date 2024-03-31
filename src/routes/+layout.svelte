<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	let online : boolean = false;
	onMount(()=>{
		window.addEventListener('online',()=>{
			online = true;
		})
		window.addEventListener('offline',()=>{
			online = false;
		})
	})
</script>

<svelte:head>
	{#if online}
		<link rel="icon" href="/relou_online.png" />
	{:else}
		<link rel="icon" href="/relou_offline.png" />
	{/if}
</svelte:head>

<div class="app">

	<main>
		<slot />
	</main>
</div>

