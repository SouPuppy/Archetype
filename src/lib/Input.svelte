<script lang="ts">
  import X from "@lucide/svelte/icons/x";

  export let placeholder: string = "Search";
  export let onSearch: (query: string) => void = () => {};
  export let mode: "input" | "submit" = "input";
  export let clearable: boolean = true;

  let query = "";

  function handleInput() {
    if (mode === "input") {
      onSearch(query);
    }
  }

  function handleSubmit(e: Event) {
    e.preventDefault();
    if (mode === "submit") {
      onSearch(query.trim());
    }
  }

  function handleClear() {
    query = "";
    onSearch("");
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="relative max-w-xs w-full">
<input
  type="text"
  name="q"
  bind:value={query}
  {placeholder}
  on:input={handleInput}
  autocomplete="off"
  autocorrect="off"
  autocapitalize="off"
  spellcheck={false}
  class="text-sm px-1 py-0.5 border-b border-solid border-gray-300 
         focus:border-blue-600 hover:border-blue-500 hover:border-b-2 
         outline-none transition w-full"
/>


  {#if clearable && query}
    <button
      type="button"
      on:click={handleClear}
      class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-600 group"
    >
      <X class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
    </button>
  {/if}
</form>
