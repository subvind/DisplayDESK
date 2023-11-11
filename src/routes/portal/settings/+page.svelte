<script lang="ts">
  import { onMount } from "svelte";

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

<div class="card">
  <div class="card-content">
    <span class="card-title">Settings</span>
    <p>This section is where members may update their contact info and profile photo. Also, manage billing information so that a subscription plan may be purchased. Licenses are for those wanting to take their social group or organization to the next level.</p>
    <br />
    <p>Fill out a task if you have a request for us. Be sure to read the F.A.Q. for details. Feel free to use our contact center for additional support.</p>
  </div>
  <div class="card-action">
    <a href="/contact-center">Contact Center</a>
  </div>
</div>