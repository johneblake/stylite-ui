<script lang="ts">
  export let value: string | number = 0;
  export let label: string = '';
</script>

<div class={`relative ${$$restProps.class}`}>
  <label
    for={label}
    class="absolute left-2 -top-3 cursor-text px-1 rounded-md
      transition-all
      text-sm text-gellert-red-500 bg-white"
  >
    {label}
  </label>
  <select
    name={label}
    bind:value
    placeholder=' '
    class={`peer block text-lg w-full appearance-none focus:outline-none`}
    on:change
  >
    <slot />
  </select>
</div>

<style lang="postcss">
  select {
    @apply border border-gellert-blue-300 rounded-md px-3 py-2;
    @apply focus:border-gellert-blue-200 hover:bg-gellert-blue-100;
  }
</style>