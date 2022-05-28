<script lang="ts">
  export let title: string | undefined = undefined;
</script>

<div class={`card ${$$restProps.class}`}>
  {#if title}
    <h2 class={`title ${$$restProps.titleClass}`}>{title}</h2>
  {/if}
  <slot />
</div>

<style lang="postcss">
  .card {
    @apply p-4 mb-2 shadow-md border border-emerald-900 rounded-md;
  }
  .title {
    @apply text-xl w-full text-emerald-900 mb-3;
  }
</style>