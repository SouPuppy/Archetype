<script lang="ts">
  import VideoCard from '$lib/VideoCard.svelte';

  const video = {
    id: 'abc123',
    title: 'Amazing Video Title',
    thumbnailUrl: '/video-placeholder.jpg',
    duration: '12:34'
  };
</script>

<VideoCard {video} />
<VideoCard {video} />
<VideoCard {video} />
