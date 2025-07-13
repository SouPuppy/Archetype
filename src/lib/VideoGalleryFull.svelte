<script lang="ts">
  import VideoGallery from './VideoGallery.svelte';

  let columnCount: number = 3;
</script>

<div class="flex flex-col md:flex-row gap-4 px-4 py-6">
  <!-- 左侧控制面板 -->
  <div class="w-full md:w-64 shrink-0 space-y-6">
    <!-- 列数选择 -->
    <div class="flex items-center gap-3">
      <span class="text-sm text-gray-700 font-medium">列数：</span>
      {#each [3, 4, 5] as n}
        <button
          on:click={() => columnCount = n}
          class={`px-3 py-1 rounded-md text-sm border transition
            ${columnCount === n
              ? 'bg-blue-500 text-white border-blue-500'
              : 'bg-gray-100 text-gray-700 border-gray-200 hover:bg-gray-200'}
          `}
        >
          {n}
        </button>
      {/each}
    </div>
  </div>

  <!-- 右侧视频展示 -->
  <div class="flex-1">
    <VideoGallery {columnCount} />
  </div>
</div>
