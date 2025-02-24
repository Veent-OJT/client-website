<script lang="ts">
  import { onMount } from 'svelte';
  import Create from './templates/createEvent/create.svelte';
  import RegistrationConfirmation from './templates/Registrar/RegistrationConfirmation.svelte';
  import type { EventData } from '$lib/types/event';

  let isRegistered = false;
  let registrationData: EventData = {
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

  function handleRegistration(event: CustomEvent<EventData>) {
    registrationData = event.detail;
    isRegistered = true;
  }
</script>

{#if !isRegistered}
  <Create on:submit={handleRegistration} />
{:else}
  <RegistrationConfirmation {registrationData} />
{/if}