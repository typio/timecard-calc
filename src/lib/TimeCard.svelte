<script>
    let daysofweek = [
        ["1", "2", "3", "4", "5", "6", "7"],
        ["Mon", "Tues", "Wed", "Thurs", "Fri", "Sat", "Sun"],
    ];

    let h12 = true;

    let days = [
        { in: "", out: "", dow: 0 },
        { in: "", out: "", dow: 1 },
        { in: "", out: "", dow: 2 },
        { in: "", out: "", dow: 3 },
        { in: "", out: "", dow: 4 },
    ];

    export let gridDim = [6, 3];
    $: col = `repeat(${gridDim[1]}, 1fr)`;
    $: row = `repeat(${gridDim[0]}, 1fr)`;

    const timeToNum = (time) => {
        if (time === "") {
            return 0;
        }
        return parseInt(time);
    };

    const interpretTime = (index, isIn) => {
        let time = isIn ? days[index].in : days[index].out;
        if (h12) {
            // handle only hour input
            if (
                Number.isInteger(parseInt(time)) &&
                parseInt(time) >= 1 &&
                parseInt(time) <= 12
            ) {
                if (isIn) days[index].in = parseInt(time) + ":00";
                else days[index].out = parseInt(time) + ":00";
                return;
            }
        } else {
            // handle only hour input
            if (
                Number.isInteger(parseInt(time)) &&
                parseInt(time) >= 0 &&
                parseInt(time) <= 23
            ) {
                if (isIn) days[index].in = parseInt(time) + ":00";
                else days[index].out = parseInt(time) + ":00";
                return;
                // interpret 24 input as 00 next day
            } else if (parseInt(time) === 24) {
                if (isIn) days[index].in = "0:00";
                else days[index].out = "0:00";
                return;
            }
        }

        // invalid input, set to nil
        if (isIn) days[index].in = "";
        else days[index].out = "";
    };

    let timeDiff = 0;
    const calcHours = () => {
        timeDiff = 0;
        days.forEach((day) => {
            timeDiff += timeToNum(day.out) - timeToNum(day.in);
        });
        // console.log(timeDiff);
    };

    const shiftDays = () => {
        days.forEach((day) => {
            day.dow = (day.dow + 1) % 7;
        });
        days = days;
    };

    const addDay = () => {
        if (days.length < 7) {
            days.push({
                in: "",
                out: "",
                dow: (days[days.length - 1].dow + 1) % 7,
            });
            gridDim[0]++;
        }
        days = days;
    };
    const removeDay = () => {
        if (days.length > 1) {
            days.pop();
            gridDim[0]--;
        }
        days = days;
    };
    const clearFields = () => {
        days.forEach((day) => {
            day.in = "";
            day.out = "";
        });
        days = days;
    };
</script>

<div>
    <div
        class="container"
        style="
        grid-template-rows: {row}; 
        grid-template-columns: {col};
    "
    >
        <div />
        <div><h3>In</h3></div>
        <div><h3>Out</h3></div>
        {#each days as day, index (index)}
            <div>
                <h3>{daysofweek[1][day.dow]}</h3>
            </div>
            <div>
                <input
                    type="text"
                    bind:value={day.in}
                    on:change={() => {
                        interpretTime(index, true);
                        calcHours();
                    }}
                />
            </div>
            <div>
                <input
                    type="text"
                    bind:value={day.out}
                    on:change={() => {
                        interpretTime(index, false);
                        calcHours();
                    }}
                />
            </div>
        {/each}
        <button on:click={shiftDays}>Shift Days</button>
        <button on:click={addDay}>Add Day</button>
        <button on:click={removeDay}>Remove Day</button>
    </div>
    <button on:click={clearFields}>Clear Fields</button>

    <div>{timeDiff}</div>
    <input type="checkbox" name="" id="12h" bind:checked={h12} />
    <label for="12h">12 Hour</label>
</div>

<style>
    .container div {
        background-color: antiquewhite;
    }

    .container {
        width: fit-content;
        min-height: fit-content;
        display: grid;
        border: 1px solid #999;
        grid-gap: 1px;
        background: #999;
    }
</style>
