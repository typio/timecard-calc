<script>
    import { selectTextOnFocus, blurOnEscape } from "./inputDirectives.js";
    import AmPmButton from "./AmPmButton.svelte";

    export let daysInWeek = 5;

    let gridDim = [daysInWeek + 1, 3];
    $: col = `repeat(${gridDim[1]}, 1fr)`;
    $: row = `repeat(${gridDim[0]}, 1fr)`;

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

    let dayName = 1;

    let h12 = true;

    let minTime = 0;

    let days = [];

    for (let i = 0; i < daysInWeek; i++) {
        days.push({ in: "", out: "", dow: i });
    }

    $: daysInAM = new Array(daysInWeek).fill(true);
    $: daysOutAM = new Array(daysInWeek).fill(false);

    const interpretTime = (
        /** @type {number} */ index,
        /** @type {boolean} */ isIn
    ) => {
        let time = isIn ? days[index].in : days[index].out;
        // selects non digits
        let regex = /[^0-9]+/g;
        time = time.replace(regex, "");

        if (h12) {
            // removes leading zeros
            time = time.replace(/\b0+/g, "");

            // handle h
            if (parseInt(time) >= 1 && parseInt(time) <= 12) {
                if (isIn) days[index].in = time + ":00";
                else days[index].out = time + ":00";
                return;
            }

            // handle hhmm
            if (
                parseInt(time.substr(0, 2)) >= 10 &&
                parseInt(time.substr(0, 2)) <= 12 &&
                parseInt(time.substr(2, 2)) >= 0 &&
                parseInt(time.substr(2, 2)) <= 59
            ) {
                // if hhm with no trailing 0
                if (time.length == 3) {
                    if (parseInt(time[2]) <= 5) time += "0";
                    else time = time.substr(0, 2) + "0" + time[2];
                }
                if (isIn)
                    days[index].in =
                        time.substr(0, 2) + ":" + time.substr(2, 2);
                else
                    days[index].out =
                        time.substr(0, 2) + ":" + time.substr(2, 2);
                return;
            }

            // handle hmm
            if (
                parseInt(time[0]) >= 1 &&
                parseInt(time[0]) <= 9 &&
                parseInt(time.substr(1, 2)) >= 0 &&
                parseInt(time.substr(1, 2)) <= 59
            ) {
                // if hm with no trailing 0
                if (time.length == 2) {
                    if (parseInt(time[1]) <= 5) time += "0";
                    else time = time[0] + "0" + time[1];
                }
                if (isIn) days[index].in = time[0] + ":" + time.substr(1, 2);
                else days[index].out = time[0] + ":" + time.substr(1, 2);
                return;
            }
        } else {
            // handle only hour input
            if (
                Number.isInteger(parseInt(time)) &&
                parseInt(time) >= 0 &&
                parseInt(time) <= 23
            ) {
                if (isIn) days[index].in = time + ":00";
                else days[index].out = time + ":00";
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

    // @ts-ignore
    $: daysInAM, daysOutAM, minTime, calcHours();

    let timeSum = 0;
    const calcHours = () => {
        timeSum = 0;
        days.forEach((day) => {
            let timeDiff = 0;
            if (day.in === "" || day.out === "") return;
            let timeIn;
            let timeOut;

            // read time
            if (h12) {
                // convert to 24h
                if (parseInt(day.in.split(":")[0]) === 12) {
                    timeIn = daysInAM[days.indexOf(day)]
                        ? "0:" + parseInt(day.in.split(":")[1])
                        : day.in;
                } else {
                    timeIn = daysInAM[days.indexOf(day)]
                        ? day.in
                        : parseInt(day.in.split(":")[0]) +
                          12 +
                          ":" +
                          day.in.split(":")[1];
                }

                if (parseInt(day.out.split(":")[0]) === 12) {
                    timeOut = daysOutAM[days.indexOf(day)]
                        ? "0:" + parseInt(day.out.split(":")[1])
                        : day.out;
                } else {
                    timeOut = daysOutAM[days.indexOf(day)]
                        ? day.out
                        : parseInt(day.out.split(":")[0]) +
                          12 +
                          ":" +
                          day.out.split(":")[1];
                }
            } else {
                timeIn = day.in;
                timeOut = day.out;
            }

            let dateIn = new Date("01/01/1970 " + timeIn);
            let dateOut = new Date("01/01/1970 " + timeOut);
            if (dateOut < dateIn) {
                dateOut.setDate(2);
            }
            timeDiff =
                Math.abs(dateIn.getTime() - dateOut.getTime()) / 1000 / 60;
            if (timeDiff < minTime * 60) {
                timeSum += minTime * 60;
                return;
            }
            timeSum += timeDiff;
        });
    };

    const shiftDays = () => {
        days.forEach((day) => {
            day.dow = (day.dow + 1) % 7;
        });
        days = days;
    };

    const addDay = () => {
        daysInWeek++;
        if (days.length < 7) {
            days.push({
                in: "",
                out: "",
                inAM: true,
                outAM: false,
                dow: (days[days.length - 1].dow + 1) % 7,
            });
            daysInAM.push(true);
            daysOutAM.push(false);
            gridDim[0]++;
        }

        days = days;
    };
    const removeDay = () => {
        if (days.length > 1) {
            days.pop();
            gridDim[0]--;
        }
        daysInAM.pop();
        daysOutAM.pop();
        days = days;
        daysInWeek--;
    };
    const clearFields = () => {
        days.forEach((day) => {
            day.in = "";
            day.out = "";
        });
        daysInAM = new Array(daysInWeek).fill(true);
        daysOutAM = new Array(daysInWeek).fill(false);
        days = days;
    };
    const dayNameCycle = () => {
        dayName = (dayName + 1) % daysofweek.length;
    };
</script>

<div>
    <div style="display: contents;" />
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
                <h3>{daysofweek[dayName][day.dow]}</h3>
            </div>
            <div>
                <input
                    type="text"
                    bind:value={day.in}
                    use:selectTextOnFocus
                    use:blurOnEscape
                    on:change={() => {
                        interpretTime(index, true);
                        calcHours();
                    }}
                />
                <div
                    class="AMPMToggle"
                    style="display: {h12 ? 'flex' : 'none'}"
                >
                    <AmPmButton
                        value={index}
                        bind:bindGroup={daysInAM}
                        on:click={calcHours}
                    />
                </div>
                <!-- {daysInAM[index] ? "AM" : "PM"} -->
            </div>
            <div>
                <input
                    type="text"
                    bind:value={day.out}
                    use:selectTextOnFocus
                    use:blurOnEscape
                    on:change={() => {
                        interpretTime(index, false);
                        calcHours();
                    }}
                />
                <div style="display: {h12 ? 'flex' : 'none'}">
                    <AmPmButton
                        value={index}
                        bind:bindGroup={daysOutAM}
                        on:click={calcHours}
                    />
                </div>
                <!-- {daysOutAM[index] ? "AM" : "PM"} -->
            </div>
        {/each}
        <button on:click={shiftDays}>Shift Days</button>
        <button on:click={addDay}>Add Day</button>
        <button on:click={removeDay}>Remove Day</button>
    </div>
    <button on:click={clearFields}>Clear Fields</button>
    <button on:click={dayNameCycle}>Change Day Naming</button>

    <label for="minTime">Minimum Hours per Day</label>
    <input type="number" id="minTime" bind:value={minTime} />

    <div>{(Math.round((timeSum / 60) * 100) / 100).toFixed(2)} hours</div>
    <div>{Math.floor(timeSum / 60)} hours {timeSum % 60} minutes</div>
    <input type="checkbox" name="" id="12h" bind:checked={h12} />
    <label for="12h">12 Hour</label>
</div>

<style>
    .container {
        width: fit-content;
        min-height: fit-content;
        display: grid;
        border: 1px solid #999;
        grid-gap: 1px;
        background: #999;
    }

    .container div {
        display: flex;
        justify-content: center;
        padding: 0;
        margin: 0;
        background-color: antiquewhite;
    }

    .container input {
        padding: 0;
        margin: 0;
        text-align: center;
        font-size: inherit;
        user-select: none;
    }
</style>
