<script>
  import CustomerAvatar from './CustomerAvatar.svelte';

  export let customer;
</script>

<div class="flex p-4">
  <CustomerAvatar
    avatar="{customer.avatar}"
    active="{customer.active}"
    membership="{customer.membership}"
    size="small"
  />

  <div class="ml-8">
    <div class="text-xl">{customer.first_name} {customer.last_name}</div>
    <div>{customer.id}</div>
  </div>
</div>
