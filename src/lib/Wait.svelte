<script lang="ts">
  export let show = false;
  /**
   * Wait will display over the content (like a dialog box does)
  */
</script>

{#if show}
  <div
    class="min-w-screen h-screen animated fadeIn faster fixed left-0 top-0 flex justify-center items-center inset-0 z-50 outline-none focus:outline-none"
  >
    <div class="relative mx-auto my-auto">
      <div class="flex justify-center items-center pt-48">
        <div class="animate-spin rounded-full h-64 w-64 border-t-4 border-b-4 border-emerald-500" />
      </div>
    </div>
  </div>
  <div class="opacity-25 fixed inset-0 z-40 bg-black" />
{/if}

<style lang="postcss">
</style>
