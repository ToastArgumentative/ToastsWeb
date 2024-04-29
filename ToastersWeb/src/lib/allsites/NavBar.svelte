<!-- src/NavBar.svelte -->
<script>
    import Toaster from "$lib/assets/Toaster.svg"
</script>

<style>
    *, *::before, *::after {
        box-sizing: border-box;
    }

    nav {
        display: flex;
        justify-content: space-between; /* Adjusts the space distribution */
        background: linear-gradient(to right, #0a0c1b, #1d1e33, #302b4e, #1d1e33, #0a0c1b);
        padding: 1rem;
        width: 100%;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        z-index: 1000;
    }
    .nav-group {
        display: flex;
        align-items: center;
    }
    .nav-icon {
        width: 40px; /* Adjust based on your nav bar's height */
        height: 40px; /* Adjust to match the width for a circle */
        border-radius: 50%; /* This makes the square image appear circular */
        object-fit: cover; /* Ensures the image covers the area well */
        padding: 5px; /* Optional: Adds some space inside the circle */
        background-color: white; /* Optional: In case your SVG has transparency */
    }
    a {
        color: white;
        text-decoration: none;
        margin: 0 10px; /* Adds some space between the links */
    }
    a:hover {
        text-decoration: underline;
    }
</style>

<nav>
    <div class="nav-group">
        <img src={Toaster} class="nav-icon" alt="Toaster" />
        <a href="/">Home</a>
        <a href="/minecraft/">Minecraft</a>

    </div>
</nav>