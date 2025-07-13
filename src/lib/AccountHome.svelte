<script lang="ts">
  import Avatar from '$lib/Avatar.svelte'; // 根据你的项目路径调整
  import { page } from '$app/stores';
  import { derived } from 'svelte/store';

  const tabs = [
    { name: 'Home', href: '/' },
    { name: 'My Posts', href: '/#' },
    { name: 'Favorites', href: '/#' }
  ];

  let query = '';
  const pathname = derived(page, ($page) => $page.url.pathname);
</script>

<div class="w-full border-b border-gray-200">
  <div class="max-w-5xl mx-auto px-6 space-y-6">
    <!-- 用户头像与名称 -->
    <div class="flex items-center gap-4 pt-6">
      <Avatar size={80} src="/avatar-fake.png" alt="User avatar" />
      <div>
        <h2 class="text-2xl font-bold">Bob</h2>
        <p class="text-gray-600">@Bob101</p>
      </div>
    </div>

    <!-- 标签栏 -->
    <div class="flex flex-wrap items-center gap-x-6">
      {#each tabs as tab}
  <a
    href={tab.href}
    class={`pb-2 text-sm font-medium transition-all ${
      $pathname === tab.href
        ? 'border-b-2 border-blue-600 text-blue-600'
        : 'text-gray-600 hover:text-gray-800'
    }`}
  >
    {tab.name}
  </a>
{/each}


      <form on:submit|preventDefault={() => query.trim() && console.log('Search:', query.trim())}>
        <input
          type="text"
          bind:value={query}
          name="q"
          placeholder="Search"
          class="border-b text-sm px-1 py-0.5 border-gray-300 focus:border-blue-600 outline-none transition"
        />
      </form>
    </div>
  </div>
</div>
