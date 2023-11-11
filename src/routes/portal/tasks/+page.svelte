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
  ];
  let organization: any;

  onMount(async () => {
		let deskHostname = window.location.hostname
		if (deskHostname === 'localhost') {
			deskHostname = 'client-area.subvind.com'
		}

    const responseOrg = await fetch(`https://api.subvind.com/organizations/deskHostname/${deskHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (responseOrg.ok) {
      organization = await responseOrg.json();
    } else {
      const errorData = await responseOrg.json();
      alert(errorData.error);
    }
    
		// @ts-ignore
		gtag('event', 'pageview', {
			'organizationId': organization.id
		});
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