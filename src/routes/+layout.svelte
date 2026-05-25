
<script lang="ts">
  import './layout.css';
  let { children } = $props();
  export const prerender = true
</script>

<svelte:head>
  <title>ShivaShakti Collection | ILAM</title>
</svelte:head>

{@render children()}
