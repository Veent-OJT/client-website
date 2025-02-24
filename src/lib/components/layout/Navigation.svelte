<script lang="ts">
  export let className = '';
  import PostsSection from '$lib/components/section/PostsSection.svelte';
  import ContactSection from '$lib/components/section/ContactSection.svelte';
  import RegisterSection from '$lib/components/section/RegisterSection.svelte';

  
  
</script>

<nav class={`hidden md:flex items-center space-x-8 ${className}`}>
  <a href="#posts" class="text-white hover:text-gray-300">Posts</a>
  <a href="#contact" class="text-white hover:text-gray-300">Contact</a>
  <a href="#register" class="text-white hover:text-gray-300 bg-red-600 px-4 py-2 rounded-md">Register</a>
</nav>

<style>     
  a {
    transition: opacity 0.3s ease-in-out;
  }
</style>
