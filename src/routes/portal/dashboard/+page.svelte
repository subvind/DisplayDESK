<script lang="ts">
  import { onMount } from "svelte";

  let active = 'dashboard'
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
<div class="container">
  <div class="card">
    <div class="card-content">
      <span class="card-title">Members Only Portal</span>
      <p>At the heart of our Members Only Portal lies a commitment to your convenience and personalization. With two primary objectives in mind, we offer a user-centric experience that revolves around tasks and settings. Your tasks provide a clear roadmap for your journey, allowing you to effortlessly manage to-do lists, stay informed about essential deadlines, and keep track of your interactions with our exclusive community. In parallel, our settings panel puts you in the driver's seat, offering the ability to customize your experience to your liking. It's all about you – ensuring that your membership experience is as tailored and rewarding as possible.</p>
    </div>
    <div class="card-action">
      <a href="/portal/tasks">Tasks</a>
      <a href="/portal/settings">Settings</a>
    </div>
  </div>
</div>