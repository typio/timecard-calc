<script>
    import TimeCards from "./lib/TimeCards.svelte";
</script>

<main>
    <div class="header">
        <h3>TimeMyCard.com</h3>
        <div class="nav-links">
            <img src="./favicons/favicon-96.png" alt="Time Card Logo" />
            <a href="#">Home</a>
        </div>
    </div>

    <div class="timecards">
        <TimeCards />
    </div>
</main>

<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }

    .header {
        display: flex;
        background-color: #f5f5f5;
        box-shadow: 0px 5px 5px #eee;
        height: 8vh;
    }

    .header h3 {
        font-family: Comfortaa, sans-serif;
        font-size: 2em;
        position: absolute;
        margin-left: 2vw;
        margin-top:4vh;
        
        transform: translateY(-50%);
    }

    .header img {
        width: 4em;
    }

    .nav-links {font-family: Comfortaa, sans-serif;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        text-decoration: none;
    }

    .nav-links a,
    .nav-links a:visited {
        padding: 0 2em 0 2em;
        text-decoration: none;
        color: #000;
    }

    .timecards {
        padding: 0;
        margin: 0;
        margin-top: 2rem;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
