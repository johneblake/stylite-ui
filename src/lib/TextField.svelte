<script lang="ts">
  export let label: string = '';
  export let value: string | number | undefined = '';
  export let readonly = false;

  let input: HTMLInputElement;
</script>

<div class={`TextField ${$$props.class}`}>
  <input
    name={label}
    type="text"
    placeholder=" "
    class="peer block text-lg w-full appearance-none focus:outline-none"
    bind:value
    bind:this={input}
    readonly={readonly}
    on:click
  />
  <label
    for={label}
    class="absolute left-2 -top-3 cursor-text px-1 rounded-md
      transition-all
      text-sm text-yellow-500 bg-white
      peer-placeholder-shown:text-base peer-placeholder-shown:text-yellow-200
      peer-placeholder-shown:top-3
      peer-focus:-top-3 peer-focus:text-yellow-500 peer-focus:text-sm
      peer-hover:bg-emerald-100"
    on:click={() => input.focus()}
  >
    {label}
  </label>
</div>

<style lang="postcss">
  input[type='text'] {
    @apply border border-emerald-300 rounded-md px-3 py-2;
    @apply hover:bg-emerald-100;
  }
  .TextField {
    @apply relative;
  }
</style>
