<script lang="ts">
	import { createEventDispatcher } from 'svelte'
	import type { Expense, User } from '../types'

	export let form: Expense
	export let users: User[] = []

	const dispatch = createEventDispatcher()

	const submit = (e: SubmitEvent) => {
		e.preventDefault()
		dispatch('submit')
	}
</script>

<form on:submit={submit} {...$$restProps}>
	<label for="title">
		Title
		<input type="text" id="title" name="title" required bind:value={form.title} />
	<label for="buyer">Who paid?</label>
	<select id="buyer" required bind:value={form.by}>
		<option value="" selected>Select a user…</option>
		{#each users as user}
			<option value={user.name}>{user.name}</option>
		{/each}
	</select>

	<fieldset>
		<legend>For whom?</legend>
		{#each users as user}
			<label for={user.name}>
				<input
					type="checkbox"
					id={user.name}
					required={!form.for.length}
					bind:group={form.for}
					value={user.name}
				/>
				{user.name}
			</label>
		{/each}
	</fieldset>

	<label for="amount">
		Amount
		<input type="number" id="amount" name="amount" required bind:value={form.amount} />
	</label>
	<button type="submit">submit</button>
</form>
