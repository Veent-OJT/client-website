<script lang="ts">
  import Logo from '../image/logo.svelte';
  import { onMount, onDestroy } from 'svelte';

  export let registrationData: {
    eventName: string;
    subdomain: string;
    startDate: string;
    startTime: string;
    endDate: string;
    endTime: string;
    location: string;
    description: string;
    companyLogo: string | null;
    poster: string | null;
    backgroundImage: string | null;
  };

  let days = 0;
  let hours = 0;
  let minutes = 0;
  let seconds = 0;
  let countdownInterval: ReturnType<typeof setInterval>;
  let isMobileMenuOpen = false;

  function updateCountdown() {
    const eventDateTime = new Date(`${registrationData.startDate}T${registrationData.startTime}`);
    const now = new Date();
    
    const diff = eventDateTime.getTime() - now.getTime();
    
    if (diff > 0) {
      days = Math.floor(diff / (1000 * 60 * 60 * 24));
      hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
      seconds = Math.floor((diff % (1000 * 60)) / 1000);
    } else {
      days = 0;
      hours = 0;
      minutes = 0;
      seconds = 0;
    }
  }

  function toggleMobileMenu() {
    isMobileMenuOpen = !isMobileMenuOpen;
  }

  onMount(() => {
    updateCountdown();
    countdownInterval = setInterval(updateCountdown, 1000);
  });

  onDestroy(() => {
    if (countdownInterval) clearInterval(countdownInterval);
  });
</script>

<div class="min-h-screen bg-[#1a1f2e] text-white">
  <!-- Fixed Header -->
  <div class="fixed top-0 left-0 right-0 z-50">
    <div class="bg-[#1a1f2e]/80 backdrop-blur-[10px]">
      <div class="max-w-6xl mx-auto px-4 py-4">
        <div class="flex justify-between items-center">
          <div>
            {#if registrationData.companyLogo}
              <img src={registrationData.companyLogo} alt="Event Logo" class="h-8" />
            {/if}
          </div>

          <button 
          class="md:hidden text-white p-2"
          on:click={toggleMobileMenu}
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            {#if !isMobileMenuOpen}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            {:else}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            {/if}
            
          </svg>
        </button>
          
          <!-- Desktop Menu -->
          <div class="hidden md:flex items-center space-x-8">
            <a href="#posts" class="text-white hover:text-gray-300 text-sm">Posts</a>
            <a href="#contact" class="text-white hover:text-gray-300 text-sm">Contact</a>
            <button class="bg-red-600 hover:bg-red-700 text-white px-6 py-2 rounded text-sm">
              Register now
            </button>
          </div>

          <!-- Mobile Menu Button -->
         
        </div>

        <!-- Mobile Menu -->
        {#if isMobileMenuOpen}
          <div class="md:hidden py-4 px-2 space-y-4">
            <a href="#posts" class="block text-white hover:text-gray-300 text-sm py-2">Posts</a>
            <a href="#contact" class="block text-white hover:text-gray-300 text-sm py-2">Contact</a>
            <button class="w-full bg-red-600 hover:bg-red-700 text-white px-6 py-2 rounded text-sm">
              Register now
            </button>
          </div>
        {/if}
        
      </div>
    </div>
  </div>

  <!-- Hero Section with Background -->
  <div class="relative min-h-[600px] md:h-[800px]">
    <!-- Background image container -->
    <div 
      class="absolute inset-0 bg-cover bg-center bg-no-repeat"
      style="background-image: url({registrationData.backgroundImage});"
    >
      <div class="absolute inset-0 bg-gradient-to-b from-[#1a1f2e] via-[#1a1f2e]/70 to-[#1a1f2e]"></div>
    </div>

    <!-- Content over background -->
    <div class="relative z-10 pt-20">
      <div class="max-w-6xl mx-auto px-4">
        <!-- Event Poster - Mobile -->
        <div class="block md:hidden mb-8">
          {#if registrationData.poster}
            <img 
              src={registrationData.poster} 
              alt="Event Poster" 
              class="w-full max-w-[300px] h-auto aspect-[3/4] object-cover rounded-lg shadow-lg mx-auto"
            />
          {/if}
          
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start">
          <!-- Event Details -->
          <div class="text-center md:text-left">
            <div class="space-y-6">
              <h1 class="text-3xl md:text-5xl font-bold ">{registrationData.eventName}</h1>
              <p class="text-gray-400 text-base md:text-lg">{registrationData.description}</p>
              
              <button class="w-full md:w-auto border-white border-[1px] text-white px-8 py-3 rounded-md hover:bg-red-700 transition-colors text-lg font-semibold">
                Register Now
              </button>

              <div class="space-y-4 text-gray-300 bg-[#000000]/50 backdrop-blur-[20px] p-4 md:p-6 rounded-lg">
                <div>
                  <p class="font-semibold text-sm uppercase">Date</p>
                  <p class="text-white text-base md:text-lg">{registrationData.startDate}</p>
                </div>
                <div>
                  <p class="font-semibold text-sm uppercase">Time</p>
                  <p class="text-white text-base md:text-lg">{registrationData.startTime} - {registrationData.endTime}</p>
                </div>
                <div>
                  <p class="font-semibold text-sm uppercase">Venue</p>
                  <p class="text-white text-base md:text-lg">{registrationData.location}</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Event Poster - Desktop -->
          <div class="hidden md:block">
            {#if registrationData.poster}
              <img 
                src={registrationData.poster} 
                alt="Event Poster" 
                class="w-full h-[600px] object-cover rounded-lg shadow-[-1px_5px_10px_25px_rgba(0,0,0,0.15)]"
              />
            {/if}
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Countdown Timer -->
  <div class="bg-[#1e2c3a] py-6 md:py-8">
    <div class="max-w-2xl mx-auto px-4">
      <div class="grid grid-cols-4 gap-2 md:gap-4">
        <div class="bg-red-600 p-3 md:p-5 rounded-lg text-center">
          <div class="text-xl md:text-2xl font-bold text-white">{days}</div>
          <div class="text-[10px] md:text-xs text-white/80 uppercase">Days</div>
        </div>
        <div class="bg-red-600 p-3 md:p-4 rounded-lg text-center">
          <div class="text-xl md:text-2xl font-bold text-white">{hours}</div>
          <div class="text-[10px] md:text-xs text-white/80 uppercase">Hours</div>
        </div>
        <div class="bg-red-600 p-3 md:p-4 rounded-lg text-center">
          <div class="text-xl md:text-2xl font-bold text-white">{minutes}</div>
          <div class="text-[10px] md:text-xs text-white/80 uppercase">Minutes</div>
        </div>
        <div class="bg-red-600 p-3 md:p-4 rounded-lg text-center">
          <div class="text-xl md:text-2xl font-bold text-white">{seconds}</div>
          <div class="text-[10px] md:text-xs text-white/80 uppercase">Seconds</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Posts Section -->
  <div class="bg-[#000000] py-8 md:py-12">
    <div class="max-w-2xl mx-auto px-4 mb-[50px] md:mb-[100px]">
      <div class="text-center">
        <h2 class="text-lg font-semibold mb-4">POSTS</h2>
        <p class="text-gray-400 text-base md:text-lg">No posts yet</p>
      </div>
    </div>
  </div>

  <!-- Register Now Section -->
  <div class="bg-gradient-to-b from-[#141b24] to-[#1e2c3a] py-12 md:py-16">
    <div class="max-w-2xl mx-auto px-4 mb-[200px] md:mb-[400px]">
      <div class="text-center">
        <h2 class="text-lg font-semibold mb-4">REGISTER NOW</h2>
      </div>
    </div>
  </div>

  <!-- Contact Section -->
  <div class="bg-[#000000] py-8 md:py-12">
    <div class="max-w-2xl mx-auto px-4 mb-[50px] md:mb-[100px]">
      <div class="text-center">
        <h2 class="text-lg font-semibold mb-4">NEED HELP? CONTACT US</h2>
        <p class="text-gray-400 text-sm mt-[100px] md:mt-[150px]">For inquiries, please contact us at:</p>
        <p class="text-gray-400 text-sm">support@veent.co</p>
      </div>
    </div>
  </div>

  <!-- Powered by Section -->
  <div class="bg-gradient-to-b from-[#1e2c3a] to-[#141b24] py-6 md:py-8">
    <div class="max-w-2xl mx-auto px-4 mb-[20px] md:mb-[30px]">
      <div class="text-center">
        <div class="flex items-center justify-center">
          <Logo />
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  /* Add smooth transition for mobile menu */
  div :global(.mobile-menu-enter) {
    transition: all 0.3s ease-out;
  }
  div :global(.mobile-menu-enter-active) {
    opacity: 1;
    transform: translateY(0);
  }
  div :global(.mobile-menu-exit) {
    transition: all 0.3s ease-in;
  }
  div :global(.mobile-menu-exit-active) {
    opacity: 0;
    transform: translateY(-10px);
  }
</style>