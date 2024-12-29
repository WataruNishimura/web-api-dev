<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<main class="p-5">
	{@render children()}
</main>
