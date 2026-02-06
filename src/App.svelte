<script>
  import { onMount } from "svelte";
  import Home from "./Pages/Home.svelte";
  import Login from "./Pages/Login.svelte";
  import Register from "./Pages/Register.svelte";

  let currentPage = "home";

  onMount(() => {
    // Handle initial load
    const params = new URLSearchParams(window.location.search);
    const page = params.get("page");
    if (page) currentPage = page;

    // Handle back button
    window.onpopstate = () => {
      const params = new URLSearchParams(window.location.search);
      currentPage = params.get("page") || "home";
    };
  });

  function navigate(page) {
    currentPage = page;
    const url = new URL(window.location.href);
    url.searchParams.set("page", page);
    window.history.pushState({}, "", url);
  }
</script>

{#if currentPage === "home"}
  <Home {navigate} />
{:else if currentPage === "login"}
  <Login {navigate} />
{:else if currentPage === "register"}
  <Register {navigate} />
{/if}
