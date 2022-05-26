<script lang="ts">
  export let progress: { progress: number; message: string };
</script>

<div class="relative pt-1">
  <div class="flex mb-2 items-center justify-between">
    <div>
      <span
        class="text-xs font-semibold inline-block py-1 px-2 rounded-full text-gellert-blue-500 bg-gellert-blue-100"
      >
        {progress.message}
      </span>
    </div>
    <div class="text-right">
      <span class="text-xs font-semibold inline-block text-gellert-blue-500">
        {progress.progress}%
      </span>
    </div>
  </div>
  <div class="overflow-hidden h-2 mb-4 text-xs flex rounded bg-gellert-blue-100">
    <div
      style="width: {progress.progress}%"
      class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-gellert-blue-700"
    />
  </div>
</div>

<style lang="postcss">
</style>
