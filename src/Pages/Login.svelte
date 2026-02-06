<script>
    import { onMount } from "svelte";
    import { fly, fade } from "svelte/transition";
    import { cubicOut } from "svelte/easing";

    export let navigate;
    let visible = false;

    onMount(() => {
        visible = true;
    });
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

    {#if visible}
        <section
            class="login-section"
            in:fly={{ y: 20, duration: 400, delay: 0, easing: cubicOut }}
        >
            <div class="glass-panel login-card">
                <h1 class="headline">
                    <span class="highlight">Welcome</span> Back
                </h1>

                <form on:submit|preventDefault={() => navigate("home")}>
                    <div class="input-group">
                        <label for="email">Email</label>
                        <input
                            type="email"
                            id="email"
                            placeholder="Enter your email"
                            required
                        />
                    </div>

                    <div class="input-group">
                        <label for="password">Password</label>
                        <input
                            type="password"
                            id="password"
                            placeholder="Enter your password"
                            required
                        />
                    </div>

                    <button class="cta-button primary" type="submit">
                        <span class="btn-text">Login</span>
                    </button>

                    <button
                        class="register-link"
                        type="button"
                        on:click|preventDefault={() => navigate("register")}
                    >
                        <span class="no-account-text"
                            >Don't have an account?</span
                        > Register?
                    </button>
                </form>

                <button class="back-link" on:click={() => navigate("home")}>
                    ← Back to Home
                </button>
            </div>
        </section>
    {/if}
</main>

<style>
    /* VARIABLES (Matches Home.svelte) */
    :global(body) {
        margin: 0;
        padding: 0;
        background-color: #05001a;
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
        display: flex;
        justify-content: center;
        align-items: center;
    }

    /* TYPOGRAPHY */
    h1,
    h2,
    h3,
    h4,
    p,
    span,
    div,
    label,
    input {
        color: #ffffff;
    }

    .headline {
        font-size: 2.5rem;
        font-weight: 700;
        letter-spacing: -1px;
        margin-bottom: 2rem;
        text-align: center;
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

    /* GLASSMORPHISM */
    .glass-panel {
        background: rgba(255, 255, 255, 0.03);
        backdrop-filter: blur(20px);
        -webkit-backdrop-filter: blur(20px);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 24px;
        padding: 3rem;
        box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3);
        width: 100%;
        max-width: 400px;
        position: relative;
        overflow: hidden;
    }

    /* INPUTS */
    .input-group {
        margin-bottom: 1.5rem;
        text-align: left;
    }

    label {
        display: block;
        margin-bottom: 0.5rem;
        font-size: 0.9rem;
        color: rgba(255, 255, 255, 0.7);
    }

    input {
        width: 100%;
        padding: 1rem;
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 12px;
        color: #fff;
        font-family: inherit;
        font-size: 1rem;
        transition: all 0.3s ease;
        box-sizing: border-box;
    }

    input:focus {
        outline: none;
        background: rgba(255, 255, 255, 0.1);
        border-color: #29a19c;
        box-shadow: 0 0 0 2px rgba(41, 161, 156, 0.2);
    }

    /* BUTTONS */
    .cta-button {
        position: relative;
        padding: 1rem 2rem;
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
        width: 100%;
        margin-top: 1rem;
        margin-bottom: 1rem;
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

    /* ANIMATED BORDER GRADIENT */
    .glass-panel::before,
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

    /* LINKS */
    .register-link {
        background: none;
        border: none;
        color: #fdff84; /* Yellow Accent */
        text-decoration: underline;
        cursor: pointer;
        font-family: inherit;
        font-size: 0.9rem;
        margin-top: 1rem;
        display: block;
        width: 100%;
        text-align: center;
        opacity: 0.8;
        transition: opacity 0.3s;
    }

    .register-link:hover {
        opacity: 1;
    }

    .no-account-text {
        color: rgba(255, 255, 255, 0.7);
        text-decoration: none;
        display: inline-block;
        margin-right: 4px;
        cursor: default;
    }

    .back-link {
        background: none;
        border: none;
        color: rgba(255, 255, 255, 0.5);
        cursor: pointer;
        font-family: inherit;
        font-size: 0.9rem;
        margin-top: 2rem;
        transition: color 0.3s;
    }

    .back-link:hover {
        color: #fff;
    }

    /* FLOATING ATOMS ANIMATION (Matches Home) */
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
</style>
