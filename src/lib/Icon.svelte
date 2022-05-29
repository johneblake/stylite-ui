<script lang="ts">
  export let src: string;
</script>

<svg
  class={`Icon ${$$restProps.class}`}
  viewBox="0 0 24 24"
  fill-rule="evenodd"
  clip-rule="evenodd"
  class:disabled={$$restProps.disabled}
>
  <path d={src} />
</svg>

<style lang="postcss">
  svg.disabled {
    @apply text-gray-100;
  }
  .Icon {
    @apply fill-current text-emerald-500 w-6 h-6 inline-block stroke-current;
  }
</style>
