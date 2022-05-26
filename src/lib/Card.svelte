<script lang="ts">
  export let title: string | undefined = undefined;
</script>

<div class={`p-4 mb-2 shadow-md border border-gellert-blue-900 rounded-md ${$$restProps.class}`}>
  {#if title}
    <h2 class={`text-xl w-full text-primary mb-3 ${$$restProps.titleClass}`}>{title}</h2>
  {/if}
  <slot />
</div>