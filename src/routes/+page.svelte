<script lang="ts">
	let { data } = $props();
	let count = $state(0);
</script>

<main>
	<h1>Sportz</h1>
	<p>Server time: {data.serverTime}</p>
	<button onclick={() => count++}>Clicked {count}</button>
	<p><a href="/api/health">/api/health</a></p>
</main>
