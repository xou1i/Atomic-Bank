<script>
    import { onMount, createEventDispatcher } from "svelte";
    import { tweened } from "svelte/motion";
    import { cubicOut } from "svelte/easing";

    let y = 0;
    let visible = false;
    let heroHeight = 0;

    // Track window scroll
    function handleScroll() {
        y = window.scrollY;
        // Strictly appear ONLY after hero (approx 100vh)
        if (y > window.innerHeight - 50) {
            // Slight buffer before full transition
            visible = true;
        } else {
            visible = false;
        }
    }

    // Smooth slide animation
    // Initial state: -150% (completely off screen)
    const navY = tweened(-150, {
        duration: 500,
        easing: cubicOut,
    });

    $: navY.set(visible ? 0 : -150);

    onMount(() => {
        // Force initial check
        handleScroll();
        window.addEventListener("scroll", handleScroll);
        return () => window.removeEventListener("scroll", handleScroll);
    });

    function scrollToTop() {
        window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function scrollToSection(id) {
        const el = document.getElementById(id);
        if (el) el.scrollIntoView({ behavior: "smooth" });
    }
</script>

<nav class="navbar glass-nav" style="transform: translate(-50%, {$navY}%);">
    <div class="nav-content">
        <div
            class="logo"
            on:click={scrollToTop}
            on:keydown={scrollToTop}
            role="button"
            tabindex="0"
        >
            Atomic Bank
        </div>
        <div class="nav-links">
            <button on:click={() => scrollToSection("about")}>About Us</button>
            <button on:click={() => scrollToSection("contact")}>Contact</button>
        </div>
    </div>
</nav>

<style>
    .navbar {
        position: fixed;
        top: 20px; /* Top margin from viewport */
        left: 50%;
        transform: translateX(
            -50%
        ); /* We need height transform too, will handle via style prop + container */
        /* Due to svelte transform conflict, let's wrap or handle Y differently. 
       Actually, `translateY({$navY}%)` is efficient. 
       But we also need `translateX(-50%)` to center it horizontally.
    */
        /* Combining transforms: */
        /* We'll use a wrapper or apply both in the style attribute */
        width: auto;
        min-width: 400px;
        z-index: 1000;
        border-radius: 50px;
        padding: 0.75rem 2rem;
        display: flex;
        justify-content: center;
    }

    /* Overriding the transform in style attribute relies on specificity or manual accumulation.
     Let's fix the transform logic in script to include X:
  */

    .nav-content {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        gap: 3rem;
    }

    .logo {
        font-weight: 700;
        font-size: 1.1rem;
        color: var(--brand-dark);
        cursor: pointer;
        user-select: none;
    }

    .nav-links {
        display: flex;
        gap: 1.5rem;
    }

    .nav-links button {
        background: none;
        border: none;
        font-size: 0.95rem;
        color: var(--text-muted);
        cursor: pointer;
        transition: color 0.2s ease;
        padding: 0;
    }

    .nav-links button:hover {
        color: var(--brand-primary);
    }
</style>
