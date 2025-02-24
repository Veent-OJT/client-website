<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { eventFormStore } from '$lib/types/eventForm';
  import { goto } from '$app/navigation';
  import TextInput from '$lib/components/event/TextInput.svelte';
  import DateTimeInput from '$lib/components/event/DateTimeInput.svelte';
  import ImageUpload from '$lib/components/event/ImageUpload.svelte';
  import EventPreview from '$lib/components/event/EventPreview.svelte';
	import type { EventData } from '$lib/types/event';
  
  const dispatch = createEventDispatcher<{ submit: EventData }>();
  let isSubmitting = false;
  let error = '';

  async function handleSubmit() {
    isSubmitting = true;
    error = '';
    
    try {
      // Dispatch the form data
      dispatch('submit', $eventFormStore);
    } catch (err) {
      error = err instanceof Error ? err.message : 'Failed to create event';
      console.error('Error creating event:', err);
    } finally {
      isSubmitting = false;
    }
  }
</script>

<div class="min-h-screen bg-gray-50 py-4 md:py-8 px-4">
  <div class="max-w-5xl mx-auto bg-white rounded-lg shadow p-4 md:p-8">
    <h1 class="text-xl md:text-2xl font-bold text-red-600 mb-6">Create New Event</h1>
    
    <form on:submit|preventDefault={handleSubmit} class="space-y-6">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 md:gap-8">
        <div class="space-y-6">
          <TextInput
            label="Event Name"
            bind:value={$eventFormStore.eventName}
            required
          />

          <div class="flex items-center space-x-2">
            <TextInput
              label=""
              bind:value={$eventFormStore.subdomain}
              placeholder="subdomain"
              className="flex-1"
            />
            <span class="text-gray-500">.veent.io</span>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <DateTimeInput
              label="Start"
              bind:date={$eventFormStore.startDate}
              bind:time={$eventFormStore.startTime}
              required
            />
            <DateTimeInput
              label="End"
              bind:date={$eventFormStore.endDate}
              bind:time={$eventFormStore.endTime}
              required
            />
          </div>

          <TextInput
            label="Event Location"
            bind:value={$eventFormStore.location}
            required
          />

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Event Description</label>
            <div class="border border-gray-300 rounded-md">
              <textarea
                bind:value={$eventFormStore.description}
                rows="6"
                class="text-black w-full px-3 py-2 focus:ring-red-500 focus:border-red-500"
                required
              ></textarea>
            </div>
          </div>
        </div>

        <div class="space-y-6">
          <EventPreview formData={$eventFormStore} />

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <ImageUpload
              label="Company Logo"
              value={$eventFormStore.companyLogo}
              onChange={(value) => $eventFormStore.companyLogo = value}
            />
            <ImageUpload
              label="Poster"
              value={$eventFormStore.poster}
              onChange={(value) => $eventFormStore.poster = value}
            />
          </div>

          <ImageUpload
            label="Background Image"
            value={$eventFormStore.backgroundImage}
            onChange={(value) => $eventFormStore.backgroundImage = value}
            objectFit="cover"
          />
        </div>
      </div>

      <div class="flex justify-center mt-8">
        {#if error}
        <div class="text-red-600 text-sm mb-4 text-center">{error}</div>
        
      {/if}
      
      <button
        type="submit"
        disabled={isSubmitting}
        class="bg-red-600 text-white px-6 md:px-8 py-2 md:py-3 rounded-md hover:bg-red-700 transition-colors disabled:opacity-50 disabled:cursor-not-allowed"
      >
        {#if isSubmitting}
          Creating...
        {:else}
          Create Event
        {/if}
      </button>
      </div>
    </form>
  </div>
</div>