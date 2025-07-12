<script lang="ts">
  import X from "@lucide/svelte/icons/x";
  import { onMount, onDestroy } from "svelte";

  export let options: string[] = [];
  export let placeholder = "Type to filter...";
  export let defaultValue = "";
  export let onSelect: (value: string) => void = () => {};
  export let clearable = true;

  let query = defaultValue;
  let isOpen = false;
  let container: HTMLDivElement;
  let dropdownList: HTMLUListElement;
  let activeIndex = -1;

  $: filtered = options.filter((opt) =>
    opt.toLowerCase().includes(query.toLowerCase())
  );

  function openDropdown() {
    isOpen = true;
    activeIndex = 0;
  }

  function clearInput() {
    query = "";
    openDropdown();
  }

  function selectOption(value: string) {
    query = value;
    isOpen = false;
    onSelect(value);
  }

  function scrollToActiveItem() {
    if (!dropdownList || activeIndex < 0) return;

    const item = dropdownList.children[activeIndex] as HTMLElement;
    if (!item) return;

    const listRect = dropdownList.getBoundingClientRect();
    const itemRect = item.getBoundingClientRect();

    if (itemRect.top < listRect.top) {
      dropdownList.scrollTop -= listRect.top - itemRect.top;
    } else if (itemRect.bottom > listRect.bottom) {
      dropdownList.scrollTop += itemRect.bottom - listRect.bottom;
    }
  }

  function handleKeydown(event: KeyboardEvent) {
    if (!isOpen || filtered.length === 0) return;

    switch (event.key) {
      case "ArrowDown":
        activeIndex = (activeIndex + 1) % filtered.length;
        event.preventDefault();
        scrollToActiveItem();
        break;
      case "ArrowUp":
        activeIndex = (activeIndex - 1 + filtered.length) % filtered.length;
        event.preventDefault();
        scrollToActiveItem();
        break;
      case "Enter":
        event.preventDefault();
        if (activeIndex >= 0 && activeIndex < filtered.length) {
          selectOption(filtered[activeIndex]);
        }
        break;
      case "Escape":
        isOpen = false;
        break;
    }
  }

  function handleClickOutside(event: MouseEvent) {
    if (!container?.contains(event.target as Node)) {
      isOpen = false;
    }
  }

  onMount(() => {
    if (typeof document !== "undefined") {
      document.addEventListener("mousedown", handleClickOutside);
      document.addEventListener("keydown", handleKeydown);
    }
  });

  onDestroy(() => {
    if (typeof document !== "undefined") {
      document.removeEventListener("mousedown", handleClickOutside);
      document.removeEventListener("keydown", handleKeydown);
    }
  });
</script>

<div class="relative w-64" bind:this={container}>
  <form on:submit|preventDefault class="relative w-48">
    <input
      type="text"
      bind:value={query}
      {placeholder}
      on:input={openDropdown}
      on:focus={() => (isOpen = true)}
      autocomplete="off"
      autocorrect="off"
      autocapitalize="off"
      spellcheck={false}
      class="border-b text-base px-1 py-0.5 pr-[28px] border-gray-300 focus:border-blue-600 outline-none transition w-48"
    />

    {#if clearable && query}
      <button
        type="button"
        on:click={clearInput}
        class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-600 group"
      >
        <X class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
      </button>
    {/if}
  </form>

  {#if isOpen}
    <ul
      bind:this={dropdownList}
      class="absolute z-10 mt-1 w-48 bg-white border border-gray-200 shadow-card rounded-none max-h-60 overflow-y-auto"
    >
      {#if filtered.length === 0}
        <li class="px-3 py-2 text-gray-400">No options</li>
      {:else}
        {#each filtered as option, i}
          <li
            role="option"
            tabindex="0"
            aria-selected={i === activeIndex}
            class="px-3 py-1 text-base cursor-pointer focus:outline-none
                {i === activeIndex
              ? 'bg-gray-100 text-blue-600'
              : 'hover:bg-gray-100'}"
            on:mousedown={() => selectOption(option)}
            on:mouseover={() => (activeIndex = i)}
            on:focus={() => (activeIndex = i)}
          >
            {option}
          </li>
        {/each}
      {/if}
    </ul>
  {/if}
</div>

<style>
  .shadow-card {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  }
</style>
