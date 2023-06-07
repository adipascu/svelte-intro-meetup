<script lang="ts">
	import { createEventDispatcher } from 'svelte'
	import type { Balance, User } from '../types'
	import Button from './Button.svelte'
	let userNameInputElement: HTMLInputElement

	export let balances: Balance[] = []

	const formatBalance = (balance: number) => {
		if (!balance) return 'is settled up'
		return (balance > 0 ? 'is owed ' : 'owes ') + Math.abs(balance)
	}

	const dispatch = createEventDispatcher<{
		add: User
	}>()
</script>

<div>
	<input placeholder="Uncle Scrooge" bind:this={userNameInputElement} />
	<Button
		on:click={(event) => {
			dispatch('add', { name: userNameInputElement.value })
			userNameInputElement.value = ''
		}}>add user</Button
	>
</div>

{#each balances as [name, balance]}
	<article>
		{name}
		{formatBalance(balance)}
	</article>
{/each}
