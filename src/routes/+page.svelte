<script lang="ts">
  import Create from './templetes/create.svelte';
  import RegistrationConfirmation from './templetes/RegistrationConfirmation.svelte'; 

  let isRegistered = false;
let registrationData = {
  eventName: '',
  subdomain: '',
  startDate: '',
  startTime: '',
  endDate: '',
  endTime: '',
  location: '',
  description: '',
  companyLogo: null,
  poster: null,
  backgroundImage: null
};

function handleRegistration(event: CustomEvent) {
  registrationData = event.detail;
  isRegistered = true;
}
</script>

{#if !isRegistered}
<Create on:submit={handleRegistration} />
{:else}
<RegistrationConfirmation {registrationData} />
{/if}
