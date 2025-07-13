<script lang="ts">
  export let size: number = 48;
  export let src: string = "/avatar-fake.png";
  export let alt: string = "avatar";
</script>

<img
  src={src}
  alt={alt}
  class="rounded-full border border-gray-300 hover:ring-1 ring-gray-300 transition box-content object-cover"
  style="width: {size}px; height: {size}px"
/>
