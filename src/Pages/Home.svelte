<script>
    import { onMount } from "svelte";
    import { fly, fade } from "svelte/transition";
    import { cubicOut } from "svelte/easing";
    import { tweened } from "svelte/motion";

    export let navigate; // Receive navigate function
    let visible = false;

    // Trusted Users Counter
    const usersCount = tweened(0, {
        duration: 2000,
        easing: cubicOut,
    });

    const transactionSpeed = tweened(0, {
        duration: 1500,
        easing: cubicOut,
    });

    let statsSection;
    let statsVisible = false;

    let observer;

    $: if (statsSection && !statsVisible) {
        observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting && !statsVisible) {
                        statsVisible = true;
                        usersCount.set(50000);
                        transactionSpeed.set(99.9);
                        observer.unobserve(entry.target);
                    }
                });
            },
            { threshold: 0.5 },
        );
        observer.observe(statsSection);
    }

    onMount(() => {
        visible = true;
    });

    const sectionDelay = 200;
</script>

<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
        href="https://fonts.googleapis.com/css2?family=Lexend:wght@100..900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<main class="atomic-app">
    <!-- Floating Background Atoms -->
    <div class="atom atom-1"></div>
    <div class="atom atom-2"></div>
    <div class="atom atom-3"></div>
    <div class="atom atom-4"></div>
    <div class="atom atom-5"></div>

    <!-- Navigation (Simple/Minimal as implied, though strict list didn't specify nav content, keeping it part of Hero or separate) -->
    <!-- Merging simplified Nav into Layout or Hero for structure -->

    <!-- 1. Hero Section -->
    {#if visible}
        <section
            class="hero"
            in:fly={{ y: 12, duration: 300, delay: 0, easing: cubicOut }}
        >
            <div class="glass-panel hero-content">
                <h1 class="headline">
                    Atomic <span class="highlight">Bank</span>
                </h1>
                <p class="subheadline">
                    The future of atomic transactions. Precise. Secure. Instant.
                </p>
                <button
                    class="cta-button primary"
                    on:click={() => navigate("login")}
                >
                    <span class="btn-text">Start Banking</span>
                </button>
            </div>
        </section>
    {/if}

    <!-- 2. Revolutionizing Banking -->
    {#if visible}
        <section
            class="features"
            in:fly={{
                y: 12,
                duration: 300,
                delay: sectionDelay,
                easing: cubicOut,
            }}
        >
            <h2 class="section-title">Revolutionizing Banking</h2>
            <div class="grid-3">
                <div class="card">
                    <h3>Instant Sync</h3>
                    <p>Real-time coherence across all your devices.</p>
                </div>
                <div class="card">
                    <h3>Zero Friction</h3>
                    <p>Seamless financial flows without the wait.</p>
                </div>
                <div class="card">
                    <h3>Global Access</h3>
                    <p>Your capital, available anywhere on Earth.</p>
                </div>
            </div>
        </section>
    {/if}

    <!-- 3. How It Works -->
    {#if visible}
        <section
            class="how-it-works"
            in:fly={{
                y: 12,
                duration: 300,
                delay: sectionDelay * 2,
                easing: cubicOut,
            }}
        >
            <h2 class="section-title">How It Works</h2>
            <div class="steps-container">
                <div class="step">
                    <div class="step-number">01</div>
                    <h4>Connect</h4>
                    <p>Link your verified identity securely.</p>
                </div>
                <div class="step">
                    <div class="step-number">02</div>
                    <h4>Deposit</h4>
                    <p>Transfer funds with atomic precision.</p>
                </div>
                <div class="step">
                    <div class="step-number">03</div>
                    <h4>Transact</h4>
                    <p>Experience instant global payments.</p>
                </div>
            </div>
        </section>
    {/if}

    <!-- 4. Why Choose Atomic Bank -->
    {#if visible}
        <section
            class="why-choose"
            bind:this={statsSection}
            in:fly={{
                y: 12,
                duration: 300,
                delay: sectionDelay * 3,
                easing: cubicOut,
            }}
        >
            <h2 class="section-title">Why Atomic?</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-value">
                        {Math.floor($usersCount).toLocaleString()}+
                    </div>
                    <div class="stat-label">Trusted Users</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">
                        {$transactionSpeed.toFixed(1)}%
                    </div>
                    <div class="stat-label">Uptime & Reliability</div>
                </div>
            </div>
            <div class="trust-badges">
                <span class="badge">256-bit Encryption</span>
                <span class="badge">Biometric Lock</span>
                <span class="badge">Atomic Integrity</span>
            </div>
        </section>
    {/if}

    <!-- 5. Ready to Bank Smarter -->
    {#if visible}
        <section
            class="cta-section"
            in:fly={{
                y: 12,
                duration: 300,
                delay: sectionDelay * 4,
                easing: cubicOut,
            }}
        >
            <div class="glass-panel cta-panel">
                <h2>Ready to Bank Smarter?</h2>
                <p>Join the revolution today.</p>
                <button
                    class="cta-button secondary"
                    on:click={() => navigate("login")}
                >
                    <span class="btn-text">Open Account</span>
                </button>
            </div>
        </section>
    {/if}

    <!-- 6. Footer -->
    {#if visible}
        <footer
            in:fly={{
                y: 12,
                duration: 300,
                delay: sectionDelay * 5,
                easing: cubicOut,
            }}
        >
            <p>&copy; 2026 Atomic Bank. All rights reserved.</p>
            <div class="footer-links">
                <span>Privacy</span>
                <span>Terms</span>
                <span>Security</span>
            </div>
        </footer>
    {/if}
</main>

<style>
    /* VARIABLES */
    :global(body) {
        margin: 0;
        padding: 0;
        background-color: #05001a; /* Very dark backup */
        color: #fff;
        font-family: "Lexend", sans-serif;
        overflow-x: hidden;
    }

    .atomic-app {
        position: relative;
        min-height: 100vh;
        width: 100%;
        overflow: hidden;
        background: radial-gradient(circle at 50% 0%, #006c68 0%, #022c2b 100%);
        padding-bottom: 4rem;
    }

    /* TYPOGRAPHY */
    h1,
    h2,
    h3,
    h4,
    p,
    span,
    div {
        color: #ffffff;
    }

    .headline {
        font-size: 3.5rem;
        font-weight: 700;
        letter-spacing: -1px;
        margin-bottom: 1rem;
    }

    .subheadline {
        font-size: 1.25rem;
        color: rgba(255, 255, 255, 0.8);
        font-weight: 300;
        margin-bottom: 2rem;
    }

    .highlight {
        background: linear-gradient(
            135deg,
            #fdff84 0%,
            #a3f7bf 50%,
            #29a19c 100%
        );
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }

    .section-title {
        font-size: 2rem;
        text-align: center;
        margin-bottom: 3rem;
        font-weight: 600;
        text-transform: uppercase;
        letter-spacing: 2px;
        opacity: 0.9;
    }

    /* SECTIONS */
    section {
        padding: 4rem 2rem;
        max-width: 1200px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* GLASSMORPHISM */
    .glass-panel {
        background: rgba(255, 255, 255, 0.03);
        backdrop-filter: blur(20px);
        -webkit-backdrop-filter: blur(20px);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 24px;
        padding: 4rem;
        text-align: center;
        box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3);
        width: 100%;
        max-width: 800px;
        position: relative;
        overflow: hidden;
    }

    /* CARD DESIGN */
    .card {
        background: rgba(255, 255, 255, 0.05);
        border-radius: 16px;
        padding: 2rem;
        text-align: left;
        position: relative;
        overflow: hidden;
        transition: transform 0.3s ease;
        cursor: pointer;
    }

    .card:hover {
        transform: translateY(-4px);
        background: rgba(255, 255, 255, 0.08);
    }

    /* ANIMATED BORDER GRADIENT */
    .card::before,
    .cta-button::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        border-radius: inherit;
        padding: 1px; /* border width */
        background: linear-gradient(
            90deg,
            #006c68,
            #29a19c,
            #a3f7bf,
            #fdff84,
            #006c68
        );
        background-size: 300% 300%;
        -webkit-mask:
            linear-gradient(#fff 0 0) content-box,
            linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
        animation: borderRotate 4s linear infinite;
        pointer-events: none;
    }

    @keyframes borderRotate {
        0% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
        100% {
            background-position: 0% 50%;
        }
    }

    .grid-3 {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 2rem;
        width: 100%;
    }

    .card h3 {
        font-size: 1.5rem;
        margin-bottom: 0.5rem;
        color: #fdff84;
    }

    .card p {
        color: rgba(255, 255, 255, 0.7);
        font-weight: 300;
    }

    /* BUTTONS */
    .cta-button {
        position: relative;
        padding: 1rem 3rem;
        background: rgba(255, 255, 255, 0.05);
        border: none;
        border-radius: 50px;
        color: #fff;
        font-family: inherit;
        font-weight: 600;
        font-size: 1.1rem;
        cursor: pointer;
        overflow: hidden;
        transition: all 0.3s ease;
    }

    .cta-button:hover {
        background: rgba(255, 255, 255, 0.1);
        transform: scale(1.02);
    }

    .cta-button.primary {
        background: linear-gradient(
            135deg,
            rgba(0, 108, 104, 0.8),
            rgba(41, 161, 156, 0.6)
        );
    }

    /* STEPS */
    .steps-container {
        display: flex;
        justify-content: space-between;
        gap: 2rem;
        width: 100%;
        flex-wrap: wrap;
    }

    .step {
        flex: 1;
        min-width: 250px;
        text-align: center;
        padding: 2rem;
    }

    .step-number {
        font-size: 4rem;
        font-weight: 800;
        color: rgba(253, 255, 132, 0.4);
        margin-bottom: -1rem;
        position: relative;
        z-index: 0;
    }

    .step h4 {
        font-size: 1.5rem;
        margin-bottom: 0.5rem;
        position: relative;
        z-index: 1;
    }

    .step p {
        color: rgba(255, 255, 255, 0.6);
    }

    /* STATS & BADGES */
    .stats-grid {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 3rem;
        margin-bottom: 4rem;
        width: 100%;
        text-align: center;
    }

    .stat-value {
        font-size: 3rem;
        font-weight: 700;
        color: #fdff84;
    }

    .stat-label {
        font-size: 1rem;
        color: rgba(255, 255, 255, 0.6);
        text-transform: uppercase;
        letter-spacing: 1px;
    }

    .trust-badges {
        display: flex;
        gap: 1rem;
        flex-wrap: wrap;
        justify-content: center;
    }

    .badge {
        padding: 0.5rem 1.5rem;
        background: rgba(44, 52, 55, 0.6);
        border: 1px solid rgba(253, 255, 132, 0.3);
        border-radius: 50px;
        font-size: 0.9rem;
        color: #fdff84;
    }

    /* FLOATING ATOMS ANIMATION */
    .atom {
        position: absolute;
        border-radius: 50%;
        filter: blur(80px);
        opacity: 0.4;
        z-index: 0;
        pointer-events: none;
        animation: floatAtom 15s infinite ease-in-out alternate;
    }

    .atom-1 {
        width: 400px;
        height: 400px;
        background: #006c68;
        top: -10%;
        left: -10%;
        animation-delay: 0s;
    }

    .atom-2 {
        width: 500px;
        height: 500px;
        background: #29a19c;
        bottom: 10%;
        right: -10%;
        animation-delay: -5s;
    }

    .atom-3 {
        width: 300px;
        height: 300px;
        background: #a3f7bf;
        top: 40%;
        left: 30%;
        opacity: 0.3;
        animation-delay: -10s;
    }

    .atom-4 {
        width: 200px;
        height: 200px;
        background: #a3f7bf;
        top: 15%;
        right: 15%;
        opacity: 0.25;
        animation-delay: -2s;
    }

    .atom-5 {
        width: 350px;
        height: 350px;
        background: #fdff84;
        bottom: 5%;
        left: 10%;
        opacity: 0.2;
        animation-delay: -7s;
    }

    @keyframes floatAtom {
        0% {
            transform: translate(0, 0);
        }
        100% {
            transform: translate(30px, 50px);
        }
    }

    /* FOOTER */
    footer {
        text-align: center;
        padding-top: 4rem;
        border-top: 1px solid rgba(255, 255, 255, 0.05);
        color: rgba(255, 255, 255, 0.4);
        width: 80%;
        margin: 0 auto;
    }

    .footer-links {
        display: flex;
        justify-content: center;
        gap: 2rem;
        margin-top: 1rem;
        font-size: 0.9rem;
    }

    .footer-links span {
        cursor: pointer;
        transition: color 0.3s;
    }

    .footer-links span:hover {
        color: #29a19c;
    }

    /* RESPONSIVE */
    @media (max-width: 768px) {
        .headline {
            font-size: 2.5rem;
        }
        .grid-3 {
            grid-template-columns: 1fr;
        }
        .steps-container {
            flex-direction: column;
        }
    }
</style>
