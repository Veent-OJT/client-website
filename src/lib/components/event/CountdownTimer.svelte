<script lang="ts">
    import type { CountdownData } from '$lib/types/event';
    import TimeBlock from './TimeBlock.svelte';
    
    export let countdown: CountdownData = {
    days: 0,
    hours: 0,
    minutes: 0,
    seconds: 0
  };
  export let isEventStarted: boolean = false;
  export let isEventEnded: boolean = false;
</script>
  
<div class="bg-[#1e2c3a] py-8">
  <div class="max-w-3xl mx-auto px-8 bg-[#1a242f] rounded-lg shadow-lg p-6">
    <div class="flex items-center justify-between">
      <div class="text-white  text-lg">
        {#if isEventEnded}
          Event ended
        {:else if isEventStarted}
          Event ends in
        {:else}
          Events starts in
        {/if}
      </div>

      <div class="flex space-x-8">
        <div class="flex flex-col items-center">
          <span class="text-gray-400 text-sm mb-2">DAYS</span>
          <div class="bg-red-600 text-white text-3xl font-bold rounded-md w-16 h-16 flex items-center justify-center">
            {countdown.days}
          </div>
        </div>

        <div class="flex flex-col items-center">
          <span class="text-gray-400 text-sm mb-2">HOURS</span>
          <div class="bg-red-600 text-white text-3xl font-bold rounded-md w-16 h-16 flex items-center justify-center">
            {countdown.hours}
          </div>
        </div>

        <div class="flex flex-col items-center">
          <span class="text-gray-400 text-sm mb-2">MINUTES</span>
          <div class="bg-red-600 text-white text-3xl font-bold rounded-md w-16 h-16 flex items-center justify-center">
            {countdown.minutes}
          </div>
        </div>

        <div class="flex flex-col items-center">
          <span class="text-gray-400 text-sm mb-2">SECONDS</span>
          <div class="bg-red-600 text-white text-3xl font-bold rounded-md w-16 h-16 flex items-center justify-center">
            {countdown.seconds}
          </div>
        </div>
      </div>
    </div>
  </div>
</div>