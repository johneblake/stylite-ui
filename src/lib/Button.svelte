<script lang="ts">
  export let disabled = false;
</script>

<button type="button" class:disabled={disabled} on:click class={`${$$restProps.class}`}>
  <slot></slot>
</button>

<style lang="postcss">
  button[type='button'] {
    @apply border border-gellert-blue-500 rounded-md shadow-md px-3 py-2;
    @apply hover:bg-gellert-blue-100;
    @apply active:bg-gellert-blue-300 transition duration-150 ease-in-out;
  }

  button.disabled {
    @apply border border-gellert-blue-300 rounded-md shadow-none px-3 py-2;
    @apply bg-gellert-blue-100 text-gray-400 pointer-events-none cursor-pointer;
  }
</style>

