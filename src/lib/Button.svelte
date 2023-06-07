<script lang="ts">
	export let outline = false
	let clazz: string
	export { clazz as class }
</script>

<button class={outline ? clazz + ' outline' : clazz} on:click>
	<slot />
</button>

<style>
	button {
		text-transform: uppercase;
	}
</style>
