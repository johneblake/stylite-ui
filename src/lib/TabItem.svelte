<script lang="ts">
  export let activeTab: number;
  export let index: number;
</script>

{#if activeTab === index}
  <slot />
{/if}

<style>
</style>
