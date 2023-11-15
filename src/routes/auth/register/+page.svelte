<script lang="ts">
  import { onMount } from "svelte";

  import { AuthAccountRegister } from "subvind-components"

	let organization: any;

  onMount(async () => {
    let deskHostname = window.location.hostname
    if (deskHostname === 'localhost') {
      deskHostname = 'client-area.subvind.com'
    }
    const response = await fetch(`https://api.subvind.com/organizations/deskHostname/${deskHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (response.ok) {
      organization = await response.json();
    } else {
      const errorData = await response.json();
      alert(errorData.error);
    }
  })
</script>

<br />
<br />
<AuthAccountRegister organization={organization} />