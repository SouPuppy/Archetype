<script lang="ts">
  export let value: number = 0;
</script>

<div class="w-full h-[2px] bg-gray-200 rounded overflow-hidden">
  <div
    class="h-full bg-black transition-all duration-300"
    style="width: {Math.min(100, Math.max(0, value))}%"
  ></div>
</div>
