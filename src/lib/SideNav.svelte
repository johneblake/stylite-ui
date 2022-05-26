<div class="h-screen">
  <div class="flex flex-row w-full">
    <div class="w-1/4 bg-gellert-blue-200 h-screen pt-4">
      <div class="flex flex-col h-full w-full">
        <slot name="panel" />
      </div>
    </div>
    <main class="w-3/4 flex flex-col h-screen pt-4 px-4">
      <slot name="content" />
    </main>
  </div>
</div>