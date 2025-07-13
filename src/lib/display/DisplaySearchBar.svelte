<script lang="ts">
  import SearchBar from '$lib/SearchBar.svelte';

  function onSearch(e: CustomEvent<string>) {
    console.log('查询关键词：', e.detail);
  }

  function onSelect(e: CustomEvent<string>) {
    console.log('选择分类：', e.detail);
  }
</script>

<SearchBar
  placeholder="搜索内容"
  on:search={onSearch}
  on:select={onSelect}
/>
