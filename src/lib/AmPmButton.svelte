<script>
    export let value;
    export let bindGroup = [];

    const updateArray = (i) => {
        bindGroup[i] = !bindGroup[i];
    };
</script>

<label>
    <input
        type="checkbox"
        {value}
        checked={!bindGroup[value]}
        on:change={() => {
            updateArray(value);
        }}
    />
    <svg
        class="AmPmButton"
        id="AmPmButton"
        data-name="AmPmButton"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 500 500"
        ><defs
            ><style>
                .Slider {
                    fill: #fff;
                }
                .Text {
                    fill: #1a1a1a;
                }
                .Sun,
                .Moon {
                    opacity: 1;
                }
                .SunLine,
                .Moon {
                    fill: none;
                    stroke-linecap: round;
                    stroke-linejoin: round;
                    stroke-width: 12px;
                }
                .SunLine {
                    stroke-miterlimit: 10;
                }
                .Moon {
                    stroke: #fff;
                }
                .Sun {
                    stroke: #333;
                }
            </style></defs
        ><rect
            id="Background"
            class="Background"
            width="500"
            height="500"
            rx="40"
        /><path
            id="Moon"
            class="Moon"
            d="M255.23,207.06c48.55-17.55,66.67-72.2,47.7-106.86-18.51-33.82-72.22-48.39-113.25-19.37,34.22-.42,64.85,19.72,76.67,50C281.69,170.1,256.86,204.86,255.23,207.06Z"
        />
        <g id="Sun" class="Sun"
            ><circle class="SunLine" cx="250" cy="375" r="60.15" /><line
                class="SunLine"
                x1="250"
                y1="291.81"
                x2="250"
                y2="314.85"
            /><line
                class="SunLine"
                x1="208.4"
                y1="302.95"
                x2="219.93"
                y2="322.91"
            /><line
                class="SunLine"
                x1="177.95"
                y1="333.4"
                x2="197.91"
                y2="344.93"
            /><line
                class="SunLine"
                x1="166.81"
                y1="375"
                x2="189.85"
                y2="375"
            /><line
                class="SunLine"
                x1="177.95"
                y1="416.6"
                x2="197.91"
                y2="405.07"
            /><line
                class="SunLine"
                x1="208.4"
                y1="447.05"
                x2="219.93"
                y2="427.09"
            /><line
                class="SunLine"
                x1="250"
                y1="458.19"
                x2="250"
                y2="435.15"
            /><line
                class="SunLine"
                x1="291.6"
                y1="447.05"
                x2="280.07"
                y2="427.09"
            /><line
                class="SunLine"
                x1="322.05"
                y1="416.6"
                x2="302.09"
                y2="405.07"
            /><line
                class="SunLine"
                x1="333.19"
                y1="375"
                x2="310.15"
                y2="375"
            /><line
                class="SunLine"
                x1="322.05"
                y1="333.4"
                x2="302.09"
                y2="344.93"
            /><line
                class="SunLine"
                x1="291.6"
                y1="302.95"
                x2="280.07"
                y2="322.91"
            /></g
        ><rect
            id="Slider"
            class="Slider"
            x="23.09"
            y="22.35"
            width="453.82"
            height="227.65"
            rx="40"
        /><g id="AMText"
            ><path
                class="AMText"
                d="M192.54,149.28l-5.18,18.83H170.22L192.6,94.77h21.71l22.83,73.34H219.27l-5.64-18.83Zm18.63-12.36-4.56-15.58c-1.26-4.34-2.57-9.84-3.69-14.13h-.23c-1.08,4.32-2.18,9.89-3.36,14.15L195,136.92Z"
            /><path
                class="AMText"
                d="M308.81,140.06c-.34-8.89-.67-19.47-.64-30.22h-.29c-2.34,9.39-5.43,19.82-8.19,28.47l-9,28.6H277.82l-7.9-28.34c-2.37-8.64-4.8-19.06-6.62-28.73h-.23c-.36,10-.77,21.3-1.21,30.44l-1.37,27.83H245.15l4.69-73.34H272l7.15,24.51c2.32,8.41,4.59,17.63,6.22,26.22h.36c2-8.49,4.49-18.16,7-26.33l7.79-24.4h21.7l3.94,73.34H310Z"
            /></g
        ><g id="PMText"
            ><path
                class="AMText"
                d="M185.55,95.74a135.85,135.85,0,0,1,22.38-1.55c10.18,0,17.54,2,22.45,5.93,4.7,3.64,7.78,9.76,7.78,17s-2.33,13.31-6.7,17.37c-5.67,5.32-14.11,7.78-23.82,7.78a38.55,38.55,0,0,1-5.66-.38v26.26H185.55ZM202,129a25,25,0,0,0,5.51.44c8.8,0,14.24-4.45,14.24-11.89,0-6.75-4.62-10.76-13-10.76a33.06,33.06,0,0,0-6.77.54Z"
            /><path
                class="AMText"
                d="M309.24,140.06c-.34-8.89-.67-19.47-.63-30.22h-.3c-2.34,9.39-5.43,19.82-8.19,28.47l-9,28.6H278.25l-7.9-28.34c-2.36-8.64-4.8-19.06-6.62-28.73h-.23c-.36,10-.77,21.3-1.21,30.44l-1.37,27.83H245.58l4.69-73.35h22.11l7.16,24.52c2.31,8.41,4.58,17.63,6.21,26.22h.36c2-8.49,4.49-18.16,7-26.33l7.8-24.41h21.69l3.94,73.35H310.38Z"
            /></g
        ></svg
    ></label
>

<style>
    :root {
        --pm-color: #243755;
        --am-color: #ffd700;

        --anim-dur: 0.3s;
    }

    svg {
        display: flex;
        width: 3em;
        padding: 0;
        margin: 0;
    }

    label {
        padding: 0;
        margin: 0;
    }

    #AMText {
        opacity: 1;
        transition: all var(--anim-dur) ease;
    }

    #PMText {
        opacity: 0;
        transition: all var(--anim-dur) ease;
    }

    #Background {
        fill: var(--am-color);
        transition: all var(--anim-dur) ease;
    }

    #Slider {
        transition: all var(--anim-dur) ease;
    }

    input[type="checkbox"]:checked + .AmPmButton #PMText {
        opacity: 100;
        transition: all var(--anim-dur) ease;
        transform: translateY(45%);
    }

    input[type="checkbox"]:checked + .AmPmButton #Moon {
        opacity: 100;
    }

    input[type="checkbox"]:checked + .AmPmButton #AMText {
        opacity: 0;
        transition: all var(--anim-dur) ease;
        transform: translateY(45%);
    }

    input[type="checkbox"]:checked + .AmPmButton #Background {
        fill: var(--pm-color);
    }

    input[type="checkbox"]:checked + .AmPmButton #Slider {
        transform: translateY(45%);
    }

    input[type="checkbox"] {
        display: none;
    }
</style>
