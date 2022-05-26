<script lang="ts">
  import { onMount } from "svelte";
  
  import Icon from "./Icon.svelte";

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
  
  <div class="flex flex-row w-full" bind:this={active}>
    <a class="flex flex-row w-full text-2xl items-center mb-1 hover:bg-gellert-blue-100 px-4"
      on:click={setActive}
      class:selected={isSelected}
      href={link}
    >
      <Icon src={icon} class="fill-current text-gellert-red-500 mr-3" />
      {name}
    </a>
  </div>
  
  <style lang="postcss">
    .selected {
      @apply bg-gellert-blue-300;
    }
  </style>
  