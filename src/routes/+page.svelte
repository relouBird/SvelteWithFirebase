<script lang="ts">
  import DeleteButton from "../components/DeleteButton.svelte";
  import { onMount } from 'svelte';

	interface todo {
		name : string;
		done : boolean;
	}
	let active = true;
	let allList: todo[] = [];	
	let val: string ;



	function handleChange (event: Event){
		localStorage.setItem('todos',JSON.stringify(allList))
	}

	onMount(() => {
    const storedValues = localStorage.getItem('todos');
    if (storedValues) {
      allList = JSON.parse(storedValues);
    } else {
      allList =  [
		{ name : "Bienvenue a toi...", done : true },
	];
      localStorage.setItem('tableau', JSON.stringify(allList));
    }
  });



</script>

<svelte:head>
	<title>Pense-bête</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>


<section>


	<div class="w-full h-screen flex-col gap-3 flex justify-center items-center">
		<div class="flex justify-center gap-2">
			<input bind:value={val} class="border-[2.25px] pl-2.5 rounded border-[#00000061] h-9 focus:outline-none" placeholder="write..." type="text">

			<button
			on:click|preventDefault={()=>{
				if(val !== "" || val !== undefined){
					allList = [...allList,{name : val, done :false}]
					localStorage.setItem('todos',JSON.stringify(allList))
					val = "";
				}
			}}
			class="bg-[#00000061] px-2 pt-1 pb-1.5 rounded text-white">Add</button>
		</div>
		<div class="w-[310px] h-[350px] py-2 pl-2 pr-1.5 scrollbar-per overflow-y-scroll">
			{#each allList as elt}
			<div class="flex justify-between items-center">
				<div class="py-1 flex justify-start gap-2 items-center">
					<input 
					bind:checked={elt.done}
					class="block scale-125"
					 type="checkbox"
					 name=""
					 on:change={handleChange}
					   id="">
					<p class="block pb-[3px]">{elt.name}</p>
				</div>
				<DeleteButton deleteFunction={()=>{
					let index = allList.indexOf(elt)
					if(index !== -1){
						allList = allList.filter((item)=> item.name !== elt.name )
						localStorage.setItem('todos',JSON.stringify(allList))
					}
					console.log(allList)
					}} 
				/>
			</div>
			{/each}
		</div>
	</div>
</section>
