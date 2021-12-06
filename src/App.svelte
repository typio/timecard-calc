<script>
    import TimeCard from "./lib/TimeCard.svelte";
    let daysInWeek = 5;
</script>

<main>
    <TimeCard daysInWeek={daysInWeek} />
</main>

<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }
</style>
