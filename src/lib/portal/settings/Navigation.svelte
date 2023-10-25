<script lang="ts">
  import { page } from '$app/stores';

</script>

<a href="/portal/settings/contact-info" class="btn nav grey" class:black={$page.url.pathname.startsWith('/portal/settings/contact-info')}>Contact Info</a>
<a href="/portal/settings/profile-photo" class="btn nav grey" class:black={$page.url.pathname.startsWith('/portal/settings/profile-photo')}>Profile Photo</a>
<a href="/portal/settings/billing" class="btn nav grey" class:black={$page.url.pathname.startsWith('/portal/settings/billing')}>Billing</a>
<a href="/portal/settings/plans" class="btn nav grey" class:black={$page.url.pathname.startsWith('/portal/settings/plans')}>Plans</a>
<a href="/portal/settings/licenses" class="btn nav grey" class:black={$page.url.pathname.startsWith('/portal/settings/licenses')}>Licenses</a>

<style>
  .nav {
    margin: 0 0 0.5em;
    text-transform: none !important;
    width: 100%;
  }
</style>