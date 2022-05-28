<script lang="ts">
  export let checked = false;
  export let readonly = false;
</script>

<label class={`inline-flex items-center ml-4 ${$$restProps.class}`}>
  <input type="checkbox" bind:checked={checked} disabled={readonly} on:change/>
  <span class="ml-2 text-emerald-700"><slot /></span>
</label>

<style lang="postcss">
  input[type='checkbox'] {
    @apply form-checkbox border border-emerald-700 rounded-sm shadow-md px-3 py-3 h-5 w-5;
    @apply text-emerald-700 focus:ring-0;
  }
</style>