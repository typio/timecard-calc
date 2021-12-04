<script>
    import TimeCard from "./lib/TimeCard.svelte";
    let timecard = [6, 3];
</script>

<main>
    <TimeCard {timecard} />
</main>

<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }
</style>
