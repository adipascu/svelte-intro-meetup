<script lang="ts">
	import { createEventDispatcher } from 'svelte'
	import { readable } from 'svelte/store'

	export let open = false
	//add dispatch for close event
	const dispatch = createEventDispatcher()
	const close = () => {
		dispatch('close')
	}
</script>

<dialog
	{open}
	on:keydown={(e) => {
		if (e.key === 'Escape') {
			close()
		}
	}}
>
	<article>
		<slot />
		<footer>This footer is always here</footer>
	</article>
</dialog>

<style>
	dialog {
		text-align: left;
	}
</style>
