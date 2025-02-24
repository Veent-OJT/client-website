<script lang="ts">
    import PostsSection from '$lib/components/section/PostsSection.svelte';
    import ContactSection from '$lib/components/section/ContactSection.svelte';
    import RegisterSection from '$lib/components/section/RegisterSection.svelte';
  
  export let isOpen: boolean;
</script>

{#if isOpen}
  <div class="fixed inset-0 z-50 bg-[#1a1f2e]/95">
    <nav class="flex flex-col items-center justify-center h-full space-y-8">
      <a href="#posts" 
        class="text-white hover:text-gray-300 text-xl">Posts</a>
      <a href="#contact" 
        class="text-white hover:text-gray-300 text-xl">Contact</a>
      <a href="#register" 
        class="text-white hover:text-gray-300 text-xl">Register</a>
    </nav>
  </div>
{/if}

<style>
  
  div {
    transition: opacity 0.3s ease-in-out;
  }
</style>