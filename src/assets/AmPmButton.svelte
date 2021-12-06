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
        on:change={() => {updateArray(value)}}
    />
    <svg
        id="AmPmButton"
        class="AmPmButton"
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
            x="26.1"
            y="26.1"
            width="447.8"
            height="447.8"
            rx="40"
        /><g id="Sun" class="Sun"
            ><circle class="SunLine" cx="250" cy="361.95" r="53.87" /><line
                class="SunLine"
                x1="250"
                y1="287.44"
                x2="250"
                y2="308.08"
            /><line
                class="SunLine"
                x1="212.75"
                y1="297.43"
                x2="223.07"
                y2="315.3"
            /><line
                class="SunLine"
                x1="185.48"
                y1="324.7"
                x2="203.35"
                y2="335.02"
            /><line
                class="SunLine"
                x1="175.49"
                y1="361.95"
                x2="196.13"
                y2="361.95"
            /><line
                class="SunLine"
                x1="185.48"
                y1="399.2"
                x2="203.35"
                y2="388.88"
            /><line
                class="SunLine"
                x1="212.75"
                y1="426.48"
                x2="223.07"
                y2="408.6"
            /><line
                class="SunLine"
                x1="250"
                y1="436.46"
                x2="250"
                y2="415.82"
            /><line
                class="SunLine"
                x1="287.25"
                y1="426.48"
                x2="276.93"
                y2="408.6"
            /><line
                class="SunLine"
                x1="314.52"
                y1="399.2"
                x2="296.65"
                y2="388.88"
            /><line
                class="SunLine"
                x1="324.51"
                y1="361.95"
                x2="303.87"
                y2="361.95"
            /><line
                class="SunLine"
                x1="314.52"
                y1="324.7"
                x2="296.65"
                y2="335.02"
            /><line
                class="SunLine"
                x1="287.25"
                y1="297.43"
                x2="276.93"
                y2="315.3"
            /></g
        ><path
            id="Moon"
            class="Moon"
            d="M254.68,211.54c43.49-15.72,59.72-64.66,42.72-95.71C280.82,85.55,232.72,72.5,196,98.49c30.65-.37,58.09,17.66,68.67,44.76C278.39,178.44,256.14,209.57,254.68,211.54Z"
        />
        <rect
            id="Slider"
            class="Slider"
            x="46.78"
            y="46.11"
            width="406.44"
            height="203.89"
            rx="40"
        /><g id="AMText"
            ><path
                class="Text"
                d="M198.54,159.79l-4.63,16.87H178.55l20-65.69H218l20.45,65.69h-16l-5-16.87Zm16.69-11.06-4.09-14c-1.13-3.89-2.29-8.81-3.3-12.66h-.21c-1,3.87-1.95,8.86-3,12.67l-3.92,13.95Z"
            /><path
                class="Text"
                d="M302.68,151.53c-.31-8-.61-17.43-.57-27.06h-.27c-2.09,8.41-4.86,17.75-7.33,25.5l-8,25.62H274.92l-7.07-25.39c-2.12-7.74-4.31-17.07-5.93-25.73h-.21c-.32,8.94-.69,19.08-1.09,27.26l-1.22,24.93H245.66l4.2-65.69h19.8l6.41,21.95c2.08,7.53,4.1,15.79,5.57,23.49H282c1.79-7.6,4-16.27,6.25-23.59l7-21.85h19.44l3.52,65.69H303.7Z"
            /></g
        ><g id="PMText">
            <path
                class="Text"
                d="M192.28,111.84a121.72,121.72,0,0,1,20.05-1.39c9.11,0,15.7,1.78,20.1,5.31a19,19,0,0,1,7,15.19c0,6.44-2.09,11.93-6,15.56-5.08,4.76-12.64,7-21.34,7a33.82,33.82,0,0,1-5.06-.34v23.52H192.28ZM207,141.63a22,22,0,0,0,4.93.4c7.89,0,12.76-4,12.76-10.65,0-6-4.14-9.65-11.63-9.65a29.45,29.45,0,0,0-6.06.49Z"
            />
            <path
                class="Text"
                d="M303.06,151.53c-.3-8-.6-17.43-.57-27.06h-.27c-2.09,8.41-4.85,17.75-7.32,25.5l-8,25.62H275.31l-7.08-25.39c-2.12-7.74-4.3-17.07-5.93-25.73h-.21c-.32,8.94-.69,19.08-1.08,27.26l-1.23,24.93H246L250.25,111h19.8l6.41,21.95c2.07,7.53,4.1,15.79,5.57,23.49h.31c1.8-7.6,4-16.27,6.25-23.59l7-21.85H315l3.53,65.69H304.09Z"
            />
        </g></svg
    ></label
>

<style>
    :root {
        --pm-color: #243755;
        --am-color: #ffd700;

        --anim-dur: 0.3s;
    }

    svg {
        width: 4em;
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
        transform: translateY(40%);
    }

    input[type="checkbox"]:checked + .AmPmButton #Moon {
        opacity: 100;
    }

    input[type="checkbox"]:checked + .AmPmButton #AMText {
        opacity: 0;
        transition: all var(--anim-dur) ease;
        transform: translateY(40%);
    }

    input[type="checkbox"]:checked + .AmPmButton #Background {
        fill: var(--pm-color);
    }

    input[type="checkbox"]:checked + .AmPmButton #Slider {
        transform: translateY(40%);
    }

    input[type="checkbox"] {
        display: none;
    }
</style>
