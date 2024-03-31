<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	let online : boolean = false;
	onMount(()=>{
		if(navigator !== undefined){
			let onl = navigator.onLine;
			window.addEventListener('online',()=>{
			onl = true;
		})
		window.addEventListener('offline',()=>{
			onl = false;
		})
		online = onl;
		}
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

