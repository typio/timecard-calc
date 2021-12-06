<script>
    import TimeCard from "./lib/TimeCard.svelte";
    let daysInWeek = 5;
</script>

<main>
    <img src="src\assets\TimeCardLogo.png" style="width:10em" alt="Time Card Logo">
    <TimeCard daysInWeek={daysInWeek} />
</main>

<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }
</style>
