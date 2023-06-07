<script lang="ts">
	import { createEventDispatcher } from 'svelte'
	import type { Due } from '../types'
	import DueItem from './DueItem.svelte'
	export let dues: Due[]
	const dispatch = createEventDispatcher<{
		clearExpenses: void
	}>()
</script>

<h2>Dues:</h2>

{#each dues as due}
	<DueItem {due} />
{/each}

<button on:click={() => dispatch('clearExpenses')}>clear all debts</button>
