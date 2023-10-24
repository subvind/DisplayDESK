<script lang="ts">
  import { onMount } from "svelte";

  import { page } from '$app/stores';

  onMount(() => {
    // let elems = document.querySelectorAll('.tabs')
    // var instance = M.Tabs.init(elems, {});
  })
</script>

<nav class="nav-extended black">
  <div class="container">
    <div class="nav-wrapper">
      <a href="/" class="brand-logo">Client Area</a>
      <a href="#" data-target="mobile-demo" class="sidenav-trigger"><i class="material-icons">menu</i></a>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <li><a href="/portal/pricing-levels">Pricing Levels</a></li>
      </ul>
    </div>
    <div class="nav-content">
      <ul class="tabs tabs-transparent">
        <li class="tab"><a href="/portal/dashboard" class:active={$page.url.pathname.startsWith('/portal/dashboard')}>Dashboard</a></li>
        <li class="tab"><a href="/portal/tasks" class:active={$page.url.pathname.startsWith('/portal/tasks')}>Tasks</a></li>
        <li class="tab"><a href="/portal/subscription" class:active={$page.url.pathname.startsWith('/portal/subscription')}>Subscription</a></li>
        <li class="tab"><a href="/portal/settings" class:active={$page.url.pathname.startsWith('/portal/settings')}>Settings</a></li>
      </ul>
    </div>
  </div>
</nav>

<ul class="sidenav" id="mobile-demo">
  <li><a href="/pricing-levels">Pricing Levels</a></li>
</ul>

<slot></slot>

<style>
  .tabs .tab a.active {
    border-bottom: 2px solid #fff;
  }
</style>