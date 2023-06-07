<script lang="ts">
	export let outline = false
</script>

<button class:outline {...$$restProps} on:click>
	<slot />
</button>

<style>
	button {
		text-transform: uppercase;
	}
</style>
