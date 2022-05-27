<script lang="ts">
  export let checked = false;
  export let readonly = false;
  export let color = 'green';
</script>

<label class={`inline-flex items-center ml-4 ${$$restProps.class}`}>
  <input type="checkbox" style={`color: ${color}`} bind:checked={checked} disabled={readonly} on:change/>
  <span class="ml-2" style={`color: ${color}`}><slot /></span>
</label>

<style lang="postcss">
  input[type='checkbox'] {
    @apply border border-emerald-500 rounded-sm shadow-md px-3 py-3 h-5 w-5;
    @apply text-emerald-300 focus:ring-0;
  }
</style>