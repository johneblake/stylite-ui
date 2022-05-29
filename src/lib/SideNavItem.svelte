<script lang="ts">
  import { onMount } from "svelte";
  
  import Icon from "$lib/Icon.svelte";

  export let icon: string;
  export let name: string;
  export let isDefault = false;
  export let current: any = undefined;
  export let link: string;

  let active: any;

  function setActive(): void {
    current = active;
  }

  $: isSelected = current === active;

  onMount(() => {
    if (isDefault) {
      setActive();
    }
  });

</script>
  
<div class="container" bind:this={active}>
  <a class="anchor"
    on:click={setActive}
    class:selected={isSelected}
    href={link}
  >
    <Icon src={icon} />
    {name}
  </a>
</div>
  
<style lang="postcss">
  .container {
    @apply flex flex-row w-full;
  }
  .anchor {
    @apply flex flex-row w-full text-2xl items-center mb-1 hover:bg-emerald-100 px-4;
  }
  .selected {
    @apply bg-emerald-300;
  }
</style>
  