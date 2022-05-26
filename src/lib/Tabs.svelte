<script lang="ts">
  export let items: string[];
  export let activeTab = 0;
  export let events: Record<string, () => void> = {};

  function onClick(name: string, index: number): void {
    if (events[name]) {
      events[name]();
    } else {
      activeTab = index;
    }
  }
</script>

<div>
  <ul class="tabs">
    {#each items as item, i}
      <li class="tab" on:click={() => onClick(item, i)} class:tab-active={activeTab === i}>
        {item}
      </li>
    {/each}
    <li class="flex-1 border-b border-gellert-blue-500 cursor-default" />
  </ul>
</div>
<div
  class="flex flex-col flex-grow overflow-y-hidden border-l border-r border-b border-gellert-blue-500 mb-2 shadow-md"
>
  <slot />
</div>

<style lang="postcss">
  .tabs {
    @apply flex cursor-pointer;
  }
  .tab {
    @apply bg-white inline-block px-3 py-2 rounded-t-md border-b border-gellert-blue-900;
  }
  .tab-active {
    @apply border-t border-l border-r border-b-0 border-gellert-blue-900;
  }
</style>
