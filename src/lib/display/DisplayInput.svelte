<script lang="ts">
  import X from "@lucide/svelte/icons/x";

  export let value = "";
  export let placeholder = "Type...";
  export let clearable = true;
  export let onClear: (() => void) | null = null;
  export let onInput: (e: Event) => void = () => {};
  export let onFocus: (e: FocusEvent) => void = () => {};

  function clear() {
    if (onClear) {
      onClear();
    } else {
      value = "";
    }
  }
</script>

<div class="relative w-48">
  <input
    type="text"
    bind:value
    {placeholder}
    on:input={onInput}
    on:focus={onFocus}
    autocomplete="off"
    autocorrect="off"
    autocapitalize="off"
    spellcheck={false}
    class="border-b text-base px-1 py-0.5 pr-[28px] border-gray-300 focus:border-blue-600 outline-none transition w-full"
  />

  {#if clearable && value}
    <button
      type="button"
      on:click={clear}
      class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-700"
    >
      <slot name="clear-icon">
        <X class="w-4 h-4" />
      </slot>
    </button>
  {/if}
</div>
