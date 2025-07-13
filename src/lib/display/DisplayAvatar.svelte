<script>
  import Avatar from '$lib/Avatar.svelte';
</script>

<!-- 自定义图片 src -->
<Avatar size={40} src="/avatar-fake.png" alt="Fake User" />

<!-- 默认 48px -->
<Avatar />

<!-- 指定大小和 alt -->
<Avatar size={64} alt="Ruoxi Ma" />

