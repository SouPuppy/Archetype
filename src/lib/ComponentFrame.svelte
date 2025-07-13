<script lang="ts">
  export let title: string = "";
</script>

{#if title}
  <h2 class="frame-title">{title}</h2>
{/if}

<div class="frame">
  <slot />
</div>

<style>
  .frame {
    margin: 0 auto 2rem auto;
    padding: 1.5rem;
    max-width: 800px;
    background: white;
    border: 1px solid #eee;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
    border-radius: 0;

    /* ✅ 横向排列，左对齐 */
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1rem;
  }

  .frame-title {
    max-width: 800px;
    margin: 1.5rem auto 0.5rem auto;
    font-size: 1.25rem;
    font-weight: 600;
    color: #111;
    text-align: left;
  }
</style>
