<script lang="ts">
	import type { Due } from '../types'

	export let due: Due
</script>

<article>
	<strong>{due.from}</strong> owes <strong>{due.to}</strong> ${due.amount}
</article>

<style>
	strong {
		text-transform: capitalize;
	}
</style>
