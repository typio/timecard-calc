<script>
    import TimeCard from "./TimeCard.svelte";

    let daysInWeek = 5;

    let dayName = 2;

    let h12 = true;

    let minTime = 0;
    let weekNum = 2;
    let weeks = [];
    let weeksInAM = [];
    let weeksOutAM = [];
    let timeSums = [];
    let daysofweek = [
        ["1", "2", "3", "4", "5", "6", "7"],
        ["Mon", "Tues", "Wed", "Thurs", "Fri", "Sat", "Sun"],
        [
            "Monday",
            "Tuesday",
            "Wednesday",
            "Thursday",
            "Friday",
            "Saturday",
            "Sunday",
        ],
    ];

    for (let i = 0; i < weekNum; i++) {
        weeks[i] = new Array();
        for (let j = 0; j < daysInWeek; j++) {
            weeks[i].push({ in: "", out: "", dow: j });
        }
    }

    for (let i = 0; i < weeks.length; i++) {
        weeksInAM[i] = new Array(daysInWeek).fill(true);
        weeksOutAM[i] = new Array(daysInWeek).fill(false);
    }

    const clearFields = () => {
        for (let i = 0; i < weeks.length; i++) {
            for (let j = 0; j < daysInWeek; j++) {
                weeks[i][j].in = "";
                weeks[i][j].out = "";
            }
            weeksInAM[i] = new Array(daysInWeek).fill(true);
            weeksOutAM[i] = new Array(daysInWeek).fill(false);
        }
        weeks = weeks;
    };
    const dayNameCycle = () => {
        dayName = (dayName + 1) % daysofweek.length;
    };
    const addWeek = () => {
        weeks = [...weeks, new Array()];
        for (let j = 0; j < daysInWeek; j++) {
            weeks[weeks.length - 1].push({ in: "", out: "", dow: j });
        }
        weeksInAM = [...weeksInAM, new Array(daysInWeek).fill(true)];
        weeksOutAM = [...weeksOutAM, new Array(daysInWeek).fill(false)];
        timeSums = [...timeSums, new Array()];
        weekNum++;
    };
    const removeWeek = () => {
        weeks = weeks.slice(0, weeks.length - 1);
        weeksInAM = weeksInAM.slice(0, weeksInAM.length - 1);
        weeksOutAM = weeksOutAM.slice(0, weeksOutAM.length - 1);
        timeSums = timeSums.slice(0, timeSums.length - 1);
        weekNum--;
    };
</script>

<main>
    {#each weeks as week, index (index)}
        <TimeCard
            {daysInWeek}
            days={week}
            daysInAM={weeksInAM[index]}
            daysOutAM={weeksOutAM[index]}
            {h12}
            {minTime}
            {dayName}
            bind:timeSum={timeSums[index]}
        />
    {/each}
    <input type="checkbox" name="" id="12h" bind:checked={h12} />
    <label for="12h">12 Hour</label>

    <label for="minTime">Minimum Hours per Day</label>
    <input type="number" id="minTime" bind:value={minTime} />

    <button on:click={clearFields}>Clear Fields</button>
    <button on:click={dayNameCycle}>Change Day Naming</button>
    <button on:click={addWeek}>Add Week</button>
    <button on:click={removeWeek}>Remove Week</button>
    <div>
        {(
            Math.round((timeSums.reduce((a, b) => a + b, 0) / 60) * 100) / 100
        ).toFixed(2)} hours
    </div>
    <div>
        {Math.floor(timeSums.reduce((a, b) => a + b, 0) / 60)} hours {timeSums.reduce(
            (a, b) => a + b,
            0
        ) % 60} minutes
    </div>
</main>
