<script lang="ts">
  export let header = '';
  let active = false;
</script>

<div class={`${active ? 'accordion-left-active' : 'accordion-left-inactive'} ${$$restProps.class}`}>
    <header class="header" on:click={() => active = !active}>
        <span class="span">{header}</span>
        <div class="icon">
          {#if active}
            <!-- icon by feathericons.com -->
            <svg aria-hidden="true" data-reactid="281" fill="none" height="24" stroke="black" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
                <polyline points="18 15 12 9 6 15">
                </polyline>
            </svg>
          {:else}
            <svg aria-hidden="true" class="" data-reactid="266" fill="none" height="24" stroke="black" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
              <polyline points="6 9 12 15 18 9">
              </polyline>
            </svg>
          {/if}
      </div>
    </header>
    {#if active}
      <slot />
    {/if}
</div>

<style lang="postcss">
  .accordion-left-active {
    @apply border-l-2 border-emerald-500;
  }
  .accordion-left-inactive {
    @apply border-l-2 border-transparent;
  }
  .header {
    @apply flex justify-between items-center p-5 pl-8 pr-8 cursor-pointer select-none;
  }
  .span {
    @apply font-thin text-xl;
  }
  .icon {
    @apply rounded-full border w-7 h-7 flex items-center justify-center;
  }
</style>