<script lang="ts">
	export let open = false
</script>

<dialog {open}>
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
