<script>
  import { createEventDispatcher } from 'svelte';
  import CustomerAvatar from './CustomerAvatar.svelte';
  import CloseIcon from '../assets/x.svg'
  import LocationIcon from '../assets/location-marker.svg'
  import ChatIcon from '../assets/chat.svg'
  import PhoneIcon from '../assets/phone.svg'

  export let customer;

  const dispatch = createEventDispatcher();

  const onClose = () => {
    dispatch('close');
  };
</script>

<div class="p-8 bg-gray-100 sticky top-4">
  <img
    src={CloseIcon}
    alt="Search"
    class="w-8 h-8 ml-4 cursor-pointer absolute right-2 top-2"
    on:click={onClose}
  />

  <CustomerAvatar
    avatar="{customer.avatar}"
    active="{customer.active}"
    membership="{customer.membership}"
    size="medium"
  />

  <div class="mt-8 leading-loose">
    <div class="text-3xl">{customer.first_name} {customer.last_name}</div>
    <div>{customer.id}</div>

    <div>{customer.relationship.toUpperCase()}</div>
    <div>
      <a href="mailto:{customer.email_address}" class="text-blue-700">
        {customer.email_address}
      </a>
    </div>
    <div>
      <a
        href="tel:{customer.phone.replace(/[^\d+]/g, '')}"
        class="text-blue-700"
      >
        {customer.phone}
      </a>
    </div>

    <div class="flex mt-4 space-x-4">
      <button class="w-8 h-8"><img src={PhoneIcon} alt="" /></button>
      <button class="w-8 h-8"><img src={ChatIcon} alt="" /></button>
      <button class="w-8 h-8"><img src={LocationIcon} alt="" /></button>
    </div>
  </div>
</div>
