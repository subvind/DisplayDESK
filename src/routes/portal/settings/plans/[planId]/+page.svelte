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

plan