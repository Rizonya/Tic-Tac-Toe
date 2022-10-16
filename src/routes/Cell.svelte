<script lang="ts">
   	import o from '$lib/images/ноль.svg'
	import x from '$lib/images/крест.svg'
    import {fade,fly} from 'svelte/transition'

    export let value: string = ''
    export let work: boolean = false;
    $: icon = value === 'o' ? o : (value === 'x' ? x : '')
</script>
<div on:click class="cell border-separate  border-4 w-1/6 aspect-square rounded-lg bg-gradient-to-t from-gray-200 to-white border-red-100 text-center text-9xl" disabled={work}>
{#if icon!=''}
    <img transition:fade={{duration:100}} class:p-5={value=='o'} src={icon} alt={value}>
    {/if}
</div >
<style>
    
</style>