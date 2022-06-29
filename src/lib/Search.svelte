<script>
  import SearchBox from './SearchBox.svelte';
  import LoaderImage from '../assets/tail-spin.svg';
  import CustomerDetails from './CustomerDetails.svelte';
  import CustomerList from './CustomerList.svelte';

  let state = 'no_query';
  let query = '';
  let foundCustomers = [];
  let selectedCustomer = null;

  const search = async (event) => {
    query = event.detail || '';
    selectedCustomer = null;

    if (query.length > 0) {
      try {
        state = 'loading';
        foundCustomers = await fetchCustomers(query);
        state = 'results_loaded';
      } catch (e) {
        state = 'error';
      }
    } else {
      state = 'no_query';
    }
  };

  const fetchCustomers = async (query) => {
    await delay(500); // imitate real HTTP request

    const response = await fetch('/profile_data.json');
    const data = await response.json();

    const hasMatch = (value, query) =>
        value.toLowerCase().indexOf(query.toLowerCase()) !== -1;

    return data.filter(
        (item) =>
            hasMatch(item.id, query) ||
            hasMatch(item.first_name, query) ||
            hasMatch(item.last_name, query) ||
            hasMatch(item.email_address, query)
    );
  }

  const delay = (duration) => {
    return new Promise((resolve) => {
      setTimeout(() => resolve(), duration);
    });
  };

  const selectCustomer = (customer) => {
    selectedCustomer = customer;
  };
</script>

<div class="">
  <SearchBox on:search={search} />

  {#if state === 'results_loaded'}
    <div class="mx-4 my-8">
      Found {foundCustomers.length} customer(s)
    </div>

    <div class="flex pb-16">
      <div class="flex-1">
        <CustomerList
          customers={foundCustomers}
          on:select={(event) => selectCustomer(event.detail)}
        />
      </div>

      <div class="flex-initial w-1/3">
        {#if selectedCustomer}
          <CustomerDetails
            customer={selectedCustomer}
            on:close={() => selectCustomer(null)}
          />
        {/if}
      </div>
    </div>
  {/if}

  {#if state === 'loading'}
    <div class="mx-4 my-8">
      <img src={LoaderImage} alt="Loading" />
    </div>
  {/if}

  {#if state === 'error'}
    <div class="mx-4 my-8">
      Oops, something went wrong
    </div>
  {/if}
</div>
