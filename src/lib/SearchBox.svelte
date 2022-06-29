<script>
  import { createEventDispatcher } from 'svelte';
  import SearchIcon from '../assets/search.svg'

  const dispatch = createEventDispatcher();

  let query = '';

  const onQueryChange = (event) => {
    setTimeout(() => {
      const newQuery = event.target.value || '';

      if (newQuery.length >= 3 && newQuery !== query) {
        dispatch('search', newQuery);
      }

      query = newQuery;
    }, 0);
  }

  const onSearch = () => {
    dispatch('search', query);
  };
</script>

<div class="flex mx-4 my-8 items-center">
  <input
    placeholder="Customer name, ID or email..."
    on:change={onQueryChange}
    on:keyup={onQueryChange}
    class="w-full max-w-lg text-lg border border-gray-300 p-2"
  />

  <img
    src={SearchIcon}
    alt="Search"
    class="w-8 h-8 ml-4 cursor-pointer"
    on:click={onSearch}
  />
</div>
