<script lang="ts">
  export let dialog = false;
  export let title: string;
</script>

{#if dialog}
  <div
    class="min-w-screen h-screen animated fadeIn faster fixed left-0 top-0 flex justify-center items-center inset-0 z-50 outline-none focus:outline-none"
  >
    <div class={`Dialog ${$$restProps.class}`}>
      <div class="w-full px-3 py-2">{title}</div>
      <div class="rounded-md shadow-md rounded-t-none bg-white text-black p-4 w-full h-full">
        <slot />
      </div>
    </div>
  </div>
  <div class="opacity-25 fixed inset-0 z-40 bg-black" />
{/if}

<style lang="postcss">
  .Dialog {
    @apply relative mx-auto my-auto rounded-md shadow-md bg-blue-400 text-white;
  }
</style>
