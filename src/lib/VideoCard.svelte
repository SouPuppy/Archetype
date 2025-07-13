<script lang="ts">
  export type Video = {
    id: string;
    title: string;
    thumbnailUrl: string;
    duration: string;
  };

  export let video: Video;
</script>

<div class="relative w-full aspect-video overflow-hidden rounded cursor-pointer group">
  <!-- 背景图 -->
  <img
    src={video.thumbnailUrl || '/video-placeholder.jpg'}
    alt={video.title}
    class="object-cover w-full h-full absolute inset-0"
    loading="lazy"
  />

  <!-- 上下渐变蒙版 -->
  <div class="absolute inset-0 z-10 pointer-events-none opacity-0 group-hover:opacity-100 transition-opacity duration-300">
    <!-- 上部渐变 -->
    <div class="absolute top-0 left-0 w-full h-1/3 bg-gradient-to-b from-black/30 to-transparent"></div>
    <!-- 下部渐变 -->
    <div class="absolute bottom-0 left-0 w-full h-1/3 bg-gradient-to-t from-black/40 to-transparent"></div>
  </div>

  <!-- 左下角标题（hover时出现） -->
  <div class="absolute bottom-2 left-2.5 right-2 z-20 text-white text-sm font-medium truncate
              opacity-0 group-hover:opacity-100 transition-opacity duration-300">
    {video.title}
  </div>

  <!-- 右下角 duration（默认显示，hover 时隐藏） -->
  <div class="absolute bottom-1 right-2 z-20 px-1.5 py-0.5 bg-black/60 text-white text-xs font-medium rounded
              transition-opacity duration-300 group-hover:opacity-0">
    {video.duration}
  </div>
</div>
