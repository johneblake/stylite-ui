<script lang="ts">
  export let label: string = '';
  export let value: string | number | undefined = '';
  export let readonly = false;
  let textArea: HTMLTextAreaElement;
</script>

<div class={`relative ${$$props.class}`}>
  <textarea
    name={label}
    class="peer p-2 block w-full appearance-none resize-none focus:outline-none"
    placeholder=" "
    bind:value
    bind:this={textArea}
    readonly={readonly}
    on:click
  />
  {#if label}
    <label
      for={label}
      class="absolute left-2 -top-3 cursor-text px-1 rounded-md
        transition:all
        text-sm text-gellert-red-500 bg-white
        peer-placeholder-shown:text-base peer-placeholder-shown:text-gellert-red-200
        peer-placeholder-shown:top-3
        peer-focus:-top-3 peer-focus:text-gellert-red-500 peer-focus:text-sm
        peer-hover:bg-gellert-blue-100"
      on:click={() => textArea.focus()}
    >
      {label}
    </label>
  {/if}
</div>

<style lang="postcss">
  textarea {
    @apply border border-gellert-blue-300 rounded-md px-3;
    @apply hover:bg-gellert-blue-100;
  }
</style>
