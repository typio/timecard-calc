<script>
    import TimeCards from "./lib/TimeCards.svelte";
</script>

<main>
    <div class="header">
        <img src="./favicons/favicon-192.png" alt="Time Card Logo" />
        <h3>TimeMyCard.com</h3>
    </div>

    <div class="row">
        <div class="leftside">
            <div class="timecards">
                <TimeCards />
            </div>
        </div>

        <div class="rightside">
            <div class="ads" />
        </div>
    </div>

    <div class="about-text">
        <h3>About</h3>
        <hr />
        <h4>How to Use</h4>
        <ul>
            <p>Enter a time in and a time out for any given day</p>
            <p>A single number can be given for an hour (9 -> 9:00)</p>
            <p>
                Three numbers can be given for an hour and minutes (915 -> 9:15)
            </p>
            <p>
                Try other inputs! The calculator can make sense of many things
            </p>
        </ul>

        <h4>Features</h4>
        <ul>
            <p>Interprets input into h:mm format</p>
            <p>Calculates difference between any two times</p>
            <p>Supports multiple timecards</p>
            <p>Switch between 12 and 24 hour</p>
            <p>Optionally cap minimum hours per day</p>
        </ul>

        <h4>Future Features</h4>
        <ul>
            <p>Save values on reload</p>
            <p>Calculate pay for a given rate</p>
            <p>Calculate O/T</p>
            <p>Add multiple pay periods per day (for breaks)</p>
        </ul>

        <!-- <h4>About</h4>
        <ul>
            <p>This time card is very easy to use</p>
        </ul> -->
        <h6>©2021 Thomas Huber <br /> me@tohuber.com</h6>
    </div>
</main>

<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }

    .header {
        background-color: #f5f5f5;
        box-shadow: 0px 5px 5px #ddd;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .header h3 {
        font-family: Comfortaa, sans-serif;
        font-size: 2em;
        padding: 0 20px 0 20px;
    }

    .header img {
        width: 4em;
        height: 4em;
    }

    .row {
        margin-top: 2rem;
    }

    .leftside {
        float: left;
        width: 70%;
    }

    .timecards {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .rightside {
        float: left;
        width: 30%;
    }

    .ads {
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #f5f5f5;
    }

    .row:after {
        content: "";
        display: table;
        clear: both;
    }

    .about-text {
        padding: 20px;
        text-align: center;
        background-color: #f2e8cf;

        box-shadow: 0px 5px 5px #ddd;
        border-radius: 20px;
        margin: 20px auto 50px auto;
        width: 70%;
    }

    hr {
        color: #386641;
    }

    .about-text h3 {
        font-size: 2em;
        color: #386641;
    }

    .about-text h4 {
        text-align: left;
        margin: 1.2em 0 1em 2em;
        font-size: 1.6em;
        color: #386641;
    }

    .about-text p {
        text-align: left;
        font-size: 1em;
        font-weight: 600;
        word-wrap: break-word;
        color: #386641;
    }

    h6 {
        font-size: 1em;
        font-weight: 600;
        word-wrap: break-word;
        color: #386641;
    }

    @media screen and (max-width: 800px) {
        .leftside,
        .rightside {
            width: 100%;
            padding: 0;
        }
    }
</style>
