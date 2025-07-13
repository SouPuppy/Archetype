<script lang="ts">
  import ComponentFrame from "$lib/ComponentFrame.svelte";
  import DisplayInput from "$lib/display/DisplayInput.svelte";
  import DisplaySelectFilter from "$lib/display/DisplaySelectFilter.svelte";
  import DisplaySearchBar from "$lib/display/DisplaySearchBar.svelte";
  import DisplayAvatar from "$lib/display/DisplayAvatar.svelte";
  import DisplayVideoCard from "$lib/display/DisplayVideoCard.svelte";
  import DisplayProgressBar from "$lib/display/displayProgressBar.svelte";

  import DisplayVideoGallery from '$lib/display/DisplayVideoGallery.svelte';
  import DisplayVideoGalleryFull from "$lib/display/DisplayVideoGalleryFull.svelte";
  import DisplayAccountHome from "$lib/display/DisplayAccountHome.svelte";

  import Line from "$lib/Line.svelte"
</script>

<DisplayAccountHome />
<DisplayVideoGallery/>
<DisplayVideoGalleryFull />

<ComponentFrame title="Input">
  <DisplayInput />
</ComponentFrame>

<ComponentFrame title="SelectFilter">
  <DisplaySelectFilter />
</ComponentFrame>

<ComponentFrame title="SearchBar">
  <DisplaySearchBar />
</ComponentFrame>

<ComponentFrame title="Avatar">
  <DisplayAvatar />
</ComponentFrame>

<ComponentFrame title="VideoCard">
  <DisplayVideoCard />
</ComponentFrame>

<ComponentFrame title="ProgressBar">
  <DisplayProgressBar />
</ComponentFrame>

<Line />

