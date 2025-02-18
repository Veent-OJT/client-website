<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  
  const dispatch = createEventDispatcher();
  
  let formData = {
    eventName: '',
    subdomain: '',
    startDate: '',
    startTime: '',
    endDate: '',
    endTime: '',
    location: '',
    description: '',
    companyLogo: null as string | null,
    poster: null as string | null,
    backgroundImage: null as string | null
  };

  function handleFileUpload(event: Event, type: 'companyLogo' | 'poster' | 'backgroundImage') {
    const input = event.target as HTMLInputElement;
    if (input.files && input.files[0]) {
      const reader = new FileReader();
      reader.onload = (e) => {
        formData[type] = e.target?.result as string;
      };
      reader.readAsDataURL(input.files[0]);
    }
  }

  function handleSubmit() {
    dispatch('submit', formData);
  }
</script>

<div class="min-h-screen bg-gray-50 py-4 md:py-8 px-4">
  <div class="max-w-5xl mx-auto bg-white rounded-lg shadow p-4 md:p-8">
    <h1 class="text-xl md:text-2xl font-bold text-red-600 mb-6">Create New Event</h1>
    
    <form on:submit|preventDefault={handleSubmit} class="space-y-6">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 md:gap-8">
        <div class="space-y-6">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Event Name</label>
            <input
              type="text"
              bind:value={formData.eventName}
              class="text-black w-full border border-gray-300 rounded-md px-3 py-2 focus:ring-red-500 focus:border-red-500"
              required
            />
          </div>

          <div class="flex items-center space-x-2">
            <input
              type="text"
              bind:value={formData.subdomain}
              placeholder="subdomain"
              class="text-black flex-1 border border-gray-300 rounded-md px-3 py-2 focus:ring-red-500 focus:border-red-500"
            />
            <span class="text-gray-500">.veent.io</span>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Start</label>
              <div class="grid grid-cols-2 gap-2">
                <input
                  type="date"
                  bind:value={formData.startDate}
                  class="text-black border border-gray-300 rounded-md px-2 py-2 text-sm focus:ring-red-500 focus:border-red-500"
                  required
                />
                <input
                  type="time"
                  bind:value={formData.startTime}
                  class="text-black border border-gray-300 rounded-md px-2 py-2 text-sm focus:ring-red-500 focus:border-red-500"
                  required
                />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">End</label>
              <div class="grid grid-cols-2 gap-2">
                <input
                  type="date"
                  bind:value={formData.endDate}
                  class="text-black border border-gray-300 rounded-md px-2 py-2 text-sm focus:ring-red-500 focus:border-red-500"
                  required
                />
                <input
                  type="time"
                  bind:value={formData.endTime}
                  class="text-black border border-gray-300 rounded-md px-2 py-2 text-sm focus:ring-red-500 focus:border-red-500"
                  required
                />
              </div>
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Event Location</label>
            <input
              type="text"
              bind:value={formData.location}
              class="text-black w-full border border-gray-300 rounded-md px-3 py-2 focus:ring-red-500 focus:border-red-500"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Event Description</label>
            <div class="border border-gray-300 rounded-md mb-2">
              <!-- <div class="border-b border-gray-300 px-2 py-1 flex space-x-2 overflow-x-auto">
                <button type="button" class="p-1 hover:bg-gray-100 rounded">B</button>
                <button type="button" class="p-1 hover:bg-gray-100 rounded italic">I</button>
                <button type="button" class="p-1 hover:bg-gray-100 rounded underline">U</button>
                <span class="border-r border-gray-300"></span>
                <button type="button" class="p-1 hover:bg-gray-100 rounded">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                  </svg>
                </button>
              </div> -->
              <textarea
                bind:value={formData.description}
                rows="6"
                class="text-black w-full px-3 py-2 focus:ring-red-500 focus:border-red-500"
                required
              ></textarea>
            </div>
          </div>
        </div>

        <div class="space-y-6">
          <div class="border border-gray-300 rounded-lg p-4">
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-4 space-y-2 sm:space-y-0">
              <h3 class="text-lg font-medium">Preview</h3>
              <div class="flex space-x-4 text-sm">
                <button type="button" class="text-gray-600">Posts</button>
                <button type="button" class="text-gray-600">Contact</button>
                <button type="button" class="bg-red-600 text-white px-3 py-1 rounded">REGISTER</button>
              </div>
            </div>
            
            <div class="space-y-4">
              <h4 class="font-medium">{formData.eventName || 'Event Name'}</h4>
              <p class="text-sm text-gray-600">{formData.description || 'Add description here.'}</p>
              
              <div class="border-2 border-dashed border-gray-300 rounded-lg h-48 flex items-center justify-center overflow-hidden">
                {#if formData.poster}
                  <img src={formData.poster} alt="Event Poster" class="w-full h-full object-contain" />
                {:else}
                  <p class="text-gray-500">YOUR POSTER GOES HERE</p>
                {/if}
                
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Company Logo</label>
              <label class="border-2 border-dashed border-gray-300 rounded-lg p-4 h-32 flex items-center justify-center cursor-pointer overflow-hidden">
                {#if formData.companyLogo}
                  <img src={formData.companyLogo} alt="Company Logo" class="w-full h-full object-contain" />
                {:else}
                  <span class="text-gray-500">+ Add file</span>
                {/if}
                
                <input
                  type="file"
                  accept="image/*"
                  class="hidden"
                  on:change={(e) => handleFileUpload(e, 'companyLogo')}
                />
              </label>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Poster</label>
              <label class="border-2 border-dashed border-gray-300 rounded-lg p-4 h-32 flex items-center justify-center cursor-pointer overflow-hidden">
                {#if formData.poster}
                  <img src={formData.poster} alt="Event Poster" class="w-full h-full object-contain" />
                {:else}
                  <span class="text-gray-500">+ Add file</span>
                {/if}
                
                <input
                  type="file"
                  accept="image/*"
                  class="hidden"
                  on:change={(e) => handleFileUpload(e, 'poster')}
                />
              </label>
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Background Image</label>
            <label class="border-2 border-dashed border-gray-300 rounded-lg p-4 h-32 flex items-center justify-center cursor-pointer overflow-hidden">
              {#if formData.backgroundImage}
                <img src={formData.backgroundImage} alt="Background Image" class="w-full h-full object-cover" />
              {:else}
                <span class="text-gray-500">+ Add background image</span>
              {/if}
              
              <input
                type="file"
                accept="image/*"
                class="hidden"
                on:change={(e) => handleFileUpload(e, 'backgroundImage')}
              />
            </label>
          </div>
        </div>
      </div>

      <div class="flex justify-center mt-8">
        <button
          type="submit"
          class="bg-red-600 text-white px-6 md:px-8 py-2 md:py-3 rounded-md hover:bg-red-700 transition-colors"
        >Create Event
        </button>
      </div>
    </form>
  </div>
</div>