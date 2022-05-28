<script lang="ts">
</script>

<div class={`container ${$$restProps.class}`}>
  <slot />
</div>

<style lang="postcss">
  .container {
    @apply flex flex-col w-full h-full p-4;
  }
</style>