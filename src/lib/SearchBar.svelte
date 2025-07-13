<script lang="ts">
  import { onMount, onDestroy, createEventDispatcher } from 'svelte';
  import { browser } from '$app/environment';
  import X from '@lucide/svelte/icons/x';

  export let placeholder: string = "Search...";
  export let categoryOptions: string[] = ['All', 'Movies', 'Shows', 'Users'];
  export let defaultCategory: string = 'All';

  const dispatch = createEventDispatcher();

  let query = '';
  let showPopover = false;
  let category = defaultCategory;
  let container: HTMLDivElement;
  let popoverPanel: HTMLDivElement;

  function handleClickOutside(event: MouseEvent) {
    const target = event.target as Node;
    if (
      container &&
      !container.contains(target) &&
      popoverPanel &&
      !popoverPanel.contains(target)
    ) {
      showPopover = false;
    }
  }

  function handleClear() {
    query = '';
    dispatch('search', query);
  }

  function handleSelect(cat: string) {
    category = cat;
    dispatch('select', category);
  }

  function handleInput() {
    dispatch('search', query);
  }

  onMount(() => {
    if (browser) {
      document.addEventListener('mousedown', handleClickOutside);
    }
  });

  onDestroy(() => {
    if (browser) {
      document.removeEventListener('mousedown', handleClickOutside);
    }
  });
</script>

<div bind:this={container} class="w-full relative max-w-2xl mx-auto">
  <!-- 输入框 -->
  <input
    type="text"
    bind:value={query}
    on:focus={() => (showPopover = true)}
    on:input={handleInput}
    placeholder={`Search in ${category.toLowerCase()}...`}
    class="w-full px-5 py-2.5 text-sm bg-white border border-gray-100 rounded-full shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-100 placeholder:text-gray-400 transition"
  />

  <!-- 清除按钮 -->
  {#if query}
    <button
      type="button"
      on:click={handleClear}
      class="absolute right-2.5 top-1/2 -translate-y-1/2 p-1 rounded-full bg-gray-200 hover:bg-gray-300 text-gray-700 shadow-sm transition"
      aria-label="Clear search"
    >
      <X class="w-4 h-4 stroke-[1.5]" />
    </button>
  {/if}

  <!-- 下拉分类 -->
  {#if showPopover}
    <div
      bind:this={popoverPanel}
      role="listbox"
      class="absolute top-full mt-2 w-full bg-white border border-gray-100 shadow-md rounded-xl z-50"
    >
      <!-- 分类选项卡 -->
      <div class="flex border-b border-gray-200">
        {#each categoryOptions as cat, i}
          <button
            type="button"
            on:click={() => handleSelect(cat)}
            class={`flex-1 text-center py-2 text-sm font-medium transition border-b-2
              ${cat === category
                ? 'text-blue-600 border-blue-600 bg-white'
                : 'text-gray-500 border-transparent hover:text-gray-700 hover:bg-gray-50'}
              ${i === 0 ? 'rounded-tl-xl' : ''}
              ${i === categoryOptions.length - 1 ? 'rounded-tr-xl' : ''}`}
          >
            {cat}
          </button>
        {/each}
      </div>

      <!-- 底部建议或描述 -->
      <div class="p-4 text-sm text-gray-500">
        Search results or suggestions for <strong>{category}</strong>
      </div>
    </div>
  {/if}
</div>
