<script>
  import "../app.css";
  import Header from "$lib/Header.svelte";
</script>

<div class="container">
  <Header />
  <main class="pt-16">
    <div class="container mx-auto px-6 my-4">
      <slot />
    </div>
  </main>
</div>
