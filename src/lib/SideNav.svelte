<div class="container">
  <div class="navigation">
    <div class="panel-container">
      <div class="panel">
        <slot name="panel" />
      </div>
    </div>
    <main class="content">
      <slot name="content" />
    </main>
  </div>
</div>

<style lang="postcss">
  .container {
    @apply flex flex-col h-full;
  }
  .navigation {
    @apply flex flex-row w-full;
  }
  .content {
    @apply w-3/4 flex flex-col h-screen pt-4 px-4;
  }
  .panel-container {
    @apply w-1/4 bg-emerald-200 h-screen pt-4;
  }
  .panel {
    @apply flex flex-col h-full w-full;
  }
</style>