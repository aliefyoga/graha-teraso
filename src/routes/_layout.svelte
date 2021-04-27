<script>
  import Sidebar from "../components/Sidebar.svelte";
  import Topbar from "../components/Topbar.svelte";
  import Footbar from "../components/Footbar.svelte";
  import Navbar from "../components/Navbar.svelte";

  export let segment;

  console.log(segment);
</script>

<div class="wrapper">
  <Sidebar />
  <div class="main">
    <Navbar />
    <!-- <Topbar /> -->
    <main class="content">
      <slot />
    </main>
    <!-- <Footbar /> -->
  </div>
</div>

<style>
</style>
