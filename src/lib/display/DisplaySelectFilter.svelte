<script lang="ts">
  import FilterSelect from '$lib/SelectFilter.svelte';

  let selected = '';
  let fruits = [
    'Apple', 'Apricot', 'Avocado', 'Banana', 'Blackberry', 'Blueberry',
    'Boysenberry', 'Cherry', 'Coconut', 'Cranberry', 'Cucumber', 'Currant',
    'Date', 'Dragonfruit', 'Durian', 'Elderberry', 'Fig', 'Grape',
    'Grapefruit', 'Guava', 'Honeydew', 'Jackfruit', 'Kiwi', 'Kumquat',
    'Lemon', 'Lime', 'Lychee', 'Mango', 'Mangosteen', 'Mulberry',
    'Nectarine', 'Olive', 'Orange', 'Papaya', 'Passionfruit', 'Peach',
    'Pear', 'Persimmon', 'Pineapple', 'Plum', 'Pomegranate', 'Quince',
    'Raspberry', 'Starfruit', 'Strawberry', 'Tamarind', 'Tangerine',
    'Tomato', 'Ugli fruit', 'Watermelon', 'White currant', 'Yuzu'
  ];

  function onSelectFruit(value: string) {
    selected = value;
  }
</script>


<p>Selected: {selected}</p>

<FilterSelect
  options={fruits}
  placeholder="Enter a fruit"
  onSelect={onSelectFruit}
/>
