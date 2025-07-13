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
  .frame-title {
    max-width: 1200px;
    margin: 1.5rem auto 0.5rem auto;
    font-size: 1.25rem;
    font-weight: 600;
    color: #111;
    text-align: left;
  }

  .frame {
    margin: 0 auto;
    padding: 1.5rem;
    max-width: 1200px;

    /* ✅ 固定高度，不随内容扩展，出现滚动条 */
    height: calc(100vh - 6rem);

    /* ✅ 扁平直角卡片风格 */
    background: white;
    border: 1px solid #e5e7eb;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
    border-radius: 0;

    /* ✅ 超出可滚动 */
    overflow: auto;

    /* ✅ 纵向排列内部元素 */
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }
</style>
