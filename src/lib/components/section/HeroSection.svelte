<script lang="ts">
    import type { EventData } from '$lib/types/event';
    import EventDetails from '../event/EventDetails.svelte';
    import EventPoster from '../event/EventPoster.svelte';
    
    export let event: EventData;
  </script>
  
  <section class="relative min-h-screen pt-20">
    {#if event.backgroundImage}
      <div 
        class="absolute inset-0 bg-cover bg-center bg-no-repeat blur-[2px]"
        style="background-image: url({event.backgroundImage});"
      >
        <div class="absolute inset-0 bg-[#000000]/80"></div>
      </div>
    {/if}
  
    <div class="relative z-10">
      <div class="max-w-6xl mx-auto px-4 py-12">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start">
          <EventDetails {event} />
          <div class="order-first md:order-last">
            <EventPoster poster={event.poster} />
          </div>
        </div>
      </div>
    </div>
  </section>