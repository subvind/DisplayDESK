<script lang="ts">
  import { onMount } from "svelte";
  import jwt_decode from 'jwt-decode';

  let accessToken: any = undefined
  let decoded: any = undefined
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

    accessToken = localStorage.getItem('access_token');
    decoded = jwt_decode(accessToken);

    M.updateTextFields();

    var elems = document.querySelectorAll('.dropdown-trigger');
    var instances = M.Dropdown.init(elems, {
      alignment: 'right'
    });

		// @ts-ignore
		gtag('event', 'pageview', {
			'organizationId': organization.id
		});
  })
</script>

<svelte:head>
  {#if organization}
    <title>Client Area - {organization.displayName} - {organization.description}</title> 
    <meta name="description" content={organization.detail} />
  {/if}
</svelte:head>

<div class="banner">
  <br />
  <br />
  <br />
  <div class="container" style="max-width: 600px;">
    <div class="card">
      <div class="card-content">
        <h1 style="margin: 0;">Client Area</h1>
        <strong>Hello There!</strong>
        <p>Welcome to the client area; a members only portal.</p>
        <br />
        <p>Thank you for you cooperation.</p>
        <br />
        {#if accessToken}
          <a href={`/portal/dashboard`} class="waves-effect yellow black-text lighten-2 btn">dashboard</a>
          <a href="/auth/logout" class="waves-effect black white-text btn">Logout</a>
        {:else}
          <a href="/auth/login" class="waves-effect black white-text btn">Login</a>
          <a href="/auth/register" class="waves-effect black white-text btn">Register</a>
        {/if}
      </div>
    </div>
  </div>
  <br />
  <br />
  <br />
</div>

<style>
  .banner {
    background-color: #e5e5f7;
    opacity: 1;
    background-image:  linear-gradient(30deg, #9b9b9b 12%, transparent 12.5%, transparent 87%, #9b9b9b 87.5%, #9b9b9b), linear-gradient(150deg, #9b9b9b 12%, transparent 12.5%, transparent 87%, #9b9b9b 87.5%, #9b9b9b), linear-gradient(30deg, #9b9b9b 12%, transparent 12.5%, transparent 87%, #9b9b9b 87.5%, #9b9b9b), linear-gradient(150deg, #9b9b9b 12%, transparent 12.5%, transparent 87%, #9b9b9b 87.5%, #9b9b9b), linear-gradient(60deg, #9b9b9b77 25%, transparent 25.5%, transparent 75%, #9b9b9b77 75%, #9b9b9b77), linear-gradient(60deg, #9b9b9b77 25%, transparent 25.5%, transparent 75%, #9b9b9b77 75%, #9b9b9b77);
    background-size: 80px 140px;
    background-position: 0 0, 0 0, 40px 70px, 40px 70px, 0 0, 40px 70px;
    height: 100vh;
  }
  .username {
    text-transform: none;
  }
  .green {
    color: green;
    background-color: transparent !important;
  }
  .blue {
    color: #039be5;
    background-color: transparent !important;
  }
  .red {
    color: red;
    background-color: transparent !important;
  }
  .purple {
    color: purple;
    background-color: transparent !important;
  }
</style>