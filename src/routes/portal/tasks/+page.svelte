<script lang="ts">
  import { onMount } from "svelte";

  let kanban = [
    {
      name: 'new'
    },
    {
      name: 'backlog'
    },
    {
      name: 'doing'
    },
    {
      name: 'review'
    },
    {
      name: 'done'
    },
  ]
  onMount(() => {
    
  })
</script>

<br />
<div class="scroll-container">
  <div class="content">
    {#each kanban as swimlane}
      <div class="box">
        <div class="card">
          <div class="card-content">
            {swimlane.name}
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .scroll-container {
    width: 100%; /* Set the width of the container */
    overflow-x: scroll; /* Enable horizontal scrolling */
    white-space: nowrap; /* Prevent content from wrapping */
  }

  .content {
    width: auto; /* Width will be determined by the content, do not set a fixed width */
  }

  .box {
    display: inline-block;
    width: 300px; /* Adjust the width as needed */
    height: 100px; /* Adjust the height as needed */
    margin: 0 1em; /* Add some margin for spacing */
  }

</style>