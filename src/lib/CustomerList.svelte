<script>
  import CustomerListItem from './CustomerListItem.svelte';
  import {createEventDispatcher} from 'svelte';

  export let customers = [];

  const groups = ['member', 'staff', 'prospect'];

  let customersByGroup = {};

  for (const group of groups) {
    customersByGroup[group] = customers.filter(
        (item) => item.relationship === group
    );
  }

  const dispatch = createEventDispatcher();

  const onSelect = (customer) => {
    dispatch('select', customer);
  };
</script>

<div>
  {#each groups as group}
    {#if customersByGroup[group].length > 0}
      <div class="group">
        {group.toUpperCase()}
      </div>

      {#each customersByGroup[group] as item}
        <div
          on:mouseenter={() => onSelect(item)}
          class="item cursor-pointer"
        >
          <CustomerListItem customer={item} />
        </div>
      {/each}
    {/if}
  {/each}
</div>

<style>
  .group {
    @apply mt-6 px-4 py-4 sticky top-0 bg-white font-medium;
  }

  .group:first-child {
    @apply mt-0;
  }

  .item:hover {
    @apply bg-gray-100 ;
  }
</style>
