<script lang="ts">
  import Navigation from "$lib/portal/settings/Navigation.svelte";
</script>

<br />
<div class="container">
  <div class="row">
    <div class="col s12 m4">
      <Navigation />
    </div>
    <div class="col s12 m8">
      <slot></slot>
    </div>
  </div>
</div>