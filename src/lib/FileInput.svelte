<script lang="ts">
  import { mdiFileUpload } from '@mdi/js';
  import { createEventDispatcher } from 'svelte';
  import Button from '$lib/Button.svelte';
  import Icon from '$lib/Icon.svelte';

  const dispatch = createEventDispatcher();

  $: icon = $$props.disabled ? 'text-emerald-100' : 'text-emerald-500';

  function uploadFile(evt: Event): void {
    const file = (evt.target as HTMLInputElement).files?.item(0);
    (evt.target as HTMLInputElement).value = '';
    dispatch('upgradeEvent', file);
  }
</script>

<div class={`inline-block overflow-hidden relative w-64 ${$$props.class}`}>
  <Button disabled={$$props.disabled}>
    <Icon src={mdiFileUpload} class={`fill-current mr-2 ${icon}`} />
    Upload Upgrade File
  </Button>
  <input
    class="cursor-pointer absolute block py-2 px-3 w-full opacity-0 top-0 right-0"
    type="file"
    disabled={$$props.disabled}
    accept="*.agstr"
    on:change={uploadFile}
  />
</div>
