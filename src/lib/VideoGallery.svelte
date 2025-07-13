<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import { tick } from 'svelte';
  import VideoCard from '$lib/VideoCard.svelte';

  export let columnCount: number = 3;

  let videos: Video[] = [];
  let page = 1;
  let loading = false;
  let hasMore = true;
  let observer: IntersectionObserver;
  let loaderRef: HTMLDivElement;

  const MAX_PAGES = 5;
  const PAGE_SIZE = () => columnCount * 4;

  type Video = {
    id: string;
    title: string;
    thumbnailUrl: string;
    duration: string;
  };

  function generateMockVideos(page: number): Video[] {
    return Array.from({ length: PAGE_SIZE() }).map((_, i) => ({
      id: `mock-${page}-${i}`,
      title: `测试视频 ${(page - 1) * PAGE_SIZE() + i + 1}`,
      thumbnailUrl: '/video-placeholder.jpg',
      duration: '10:23',
    }));
  }

  async function loadMore() {
    if (loading || !hasMore) return;
    loading = true;
    // comment me
    await new Promise((r) => setTimeout(r, 500));
    const newVideos = generateMockVideos(page);
    videos = [...videos, ...newVideos];
    page += 1;
    if (page > MAX_PAGES) hasMore = false;
    loading = false;
  }

  function resetAndReload() {
    videos = [];
    page = 1;
    hasMore = true;
    loadMore();
  }

  $: if (columnCount) {
    resetAndReload();
  }

  onMount(async () => {
    await tick();
    observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting) {
          loadMore();
        }
      },
      { rootMargin: '300px' }
    );
    if (loaderRef) observer.observe(loaderRef);
  });

  onDestroy(() => {
    observer?.disconnect();
  });

  $: columnClass = {
    3: 'md:grid-cols-3',
    4: 'md:grid-cols-4',
    5: 'md:grid-cols-5',
  }[columnCount] ?? 'md:grid-cols-3';
</script>

<div class="rounded-xl px-4 py-6">
  <div class={`grid gap-3 grid-cols-1 sm:grid-cols-2 ${columnClass}`}>
    {#each videos as video (video.id)}
      <VideoCard {video} />
    {/each}
    {#if hasMore}
      <div
        bind:this={loaderRef}
        class="h-10 col-span-full flex justify-center items-center text-sm text-gray-500"
      >
        {loading ? '加载中...' : '加载更多'}
      </div>
    {/if}
  </div>
</div>
