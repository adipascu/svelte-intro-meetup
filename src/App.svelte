<script lang="ts">
	import Balances from './lib/Balances.svelte'
	import Dues from './lib/Dues.svelte'
	import Expenses from './lib/Expenses.svelte'
	import Button from './lib/Button.svelte'
	import { expenses, balances, dues, users } from './lib/stores'
	import type { Expense, User } from './types'

	const title = 'Bill Split'
	const views = ['expenses', 'balance', 'dues'] as const
	type View = (typeof views)[number]

	let selectedView: View = 'expenses'

	const changeView = (view: View) => () => (selectedView = view)

	const addExpense = (e: CustomEvent<Expense>) => {
		const f = e.detail
		if (!f.title || !f.amount || !f.for.length || !f.by) {
			throw new Error('incomplete data!')
		}
		expenses.update((list) => [f, ...list])
	}

	const addUser = (e: CustomEvent<User>) => {
		users.update((list) => [e.detail, ...list])
	}

	const clearDebts = () => {
		expenses.update((expenses) =>
			expenses.map((expense) => ({
				...expense,
				settled: true,
			}))
		)
	}
</script>

<main>
	<h1>{title}</h1>

	{#each views as view}
		<Button class="secondary" outline={view !== selectedView} on:click={changeView(view)}
			>{view}</Button
		>
	{/each}
	<hr />

	{#if selectedView === 'expenses'}
		<Expenses expenses={$expenses} users={$users} on:add={addExpense} />
	{:else if selectedView === 'balance'}
		<Balances balances={$balances} on:add={addUser} />
	{:else if selectedView === 'dues'}
		<Dues dues={$dues} on:clearExpenses={clearDebts} />
	{/if}
</main>
