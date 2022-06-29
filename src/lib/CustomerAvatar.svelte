<script>
  import StatusActiveIcon from '../assets/status-active.svg';
  import StatusInactiveIcon from '../assets/status-inactive.svg';

  export let avatar;
  export let active;
  export let membership;
  export let size;
</script>

<div class="relative {size}">
  <img
    src="/profile_pics/{size}/{avatar}"
    alt=""
    class="rounded-full membership-{(membership || 'regular').toLowerCase()}"
  />
  <img
    src="{active ? StatusActiveIcon : StatusInactiveIcon}"
    alt=""
    class="absolute bottom-0 right-0"
  />
</div>

<style>
  .small {
    @apply w-16 h-16;
  }

  .medium {

  }

  .membership-gold {
    @apply ring-4 ring-yellow-500/50;
  }

  .membership-silver {
    @apply ring-4 ring-gray-500/50;
  }

  .membership-platin {
    @apply ring-4 ring-purple-500/50;
  }
</style>
