<script lang="ts">
	import { confetti } from '@neoconfetti/svelte';
	import { applyAction, enhance } from '$app/forms';
	import { invalidateAll } from '$app/navigation';
	import Cell from './Cell.svelte'
	import { clear_loops, get_root_for_style, group_outros, onMount, validate_component } from 'svelte/internal';
	import { error } from '@sveltejs/kit';
	import type { fromJSON } from 'postcss';
	import { fade } from 'svelte/transition';
	let rowLen = 3;
	let colLen = 3;
	let grid = [['','',''],['','',''],['','','']]
	let xturn = true;
	let tie :boolean = false;
	let winner: string='';
	let isGameEnd:boolean = false;
	$:{
	//Checking if game was ended
		
		if(!isGameEnd){

		for(let i=0;i<3;i++){
			//Checking rows
			if((grid[i][2]==grid[i][1]&&grid[i][1]==grid[i][0]&&grid[i][1]!='')
			   ){
				winner=grid[i][1]
				isGameEnd = true
				break;
			}
			//Cheking diagonals
			if((grid[0][0]==grid[1][1]&&grid[2][2]==grid[1][1]&&grid[1][1]!='')||
			   (grid[0][2]==grid[1][1]&&grid[2][0]==grid[1][1]&&grid[1][1]!='')){
				winner = grid[1][1]
				isGameEnd = true
				break
			   }
		    //Checking cols
			if((grid[0][i]==grid[1][i]&&grid[1][i]==grid[2][i]&&grid[1][i]!='')){
				winner = grid[1][i];
				isGameEnd = true
				break
			}
			
		}
		tie = !grid.flat().some(e=>e=='')&&!isGameEnd
	}
	}
	$:{
		if(isGameEnd){
			console.log(winner+' Подебили')
		}
	}
		</script>
		
	<div transition:fade class=" flex flex-col container justify-center gap-14 content-center">
		{#if isGameEnd}
		<label class="flex flex-row justify-center items-center">

			<h2 class = 'text-3xl'>{winner.toUpperCase()} подебили.</h2>
		</label>
		{/if}
		{#if tie}
		<label class="flex flex-row justify-center items-center">

			<h2 class = 'text-3xl text-center'>Никто не подебил, все ебланы.</h2>
		</label>
		{/if}
		<div class="flex flex-col gap-3">
			{#each grid as row}
			<div class='flex flex-row items-center justify-center gap-2'>
		{#each row as cell}
			<Cell
			 on:click={()=>{
				if(!isGameEnd&&!tie){
				cell!=''?{}:xturn ? cell='x':cell='o';
				xturn=!xturn;}
			}} bind:value={cell}/>
		{/each}
	</div>
	{/each}
	
</div>
{#if isGameEnd||tie}
<div class="w-full flex flex-row justify-center rounded-md items-center">
	<button class='w-52 h-10 bg-orange-500' on:click={()=>{isGameEnd=false;grid =[['','',''],['','',''],['','','']]}}>
		новая игра
	</button>
</div>
{/if}


	</div>
<style>
</style>