# stopwatch
Stopwatch using html css and JavaScript





<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" type="text/css" href="stopwatch.css">
</head>
<body>
    <div class="stopwatch">
        <div class="display">00:00:00:000</div>
            <button id="start">Start</button>

            <button id="pauseed">Pause</button>

            <button id="reset">Reset</button>

            <button id="cast">Cast</button>

            <div class="casts">None</div>
    </div>

    <script>
        let startTime;
        let casts = [];
        let intervalTimer;
        let lapsed = 0;


        const timeFormat = (time) => {
            let mili_sec = time % 1000;
            
            time = (time-mili_sec) / 1000;

            let seconds = time % 60;

            time = (time-seconds) / 60;

            let minuits = time % 60;

            let hours = (time-minuits) / 60;

            return `${hours.toString().padStart(2, '0')} : ${minuits.toString().padStart(2, '0')} : ${seconds.toString().padStart(2, '0')} : ${mili_sec.toString().padStart(3, '0')}`
            // return `${hours.toString()}:${minuits.toString()}:${seconds.toString()}:${mili_sec.toString()}`
        }


        const displayUpdate = () =>{
            const display = document.querySelector('.display');
            display.textContent = timeFormat(lapsed);
        };

        const timerStart = (event) => {
            startTime = Date.now() - lapsed;
            intervalTimer = setInterval(() => {
                lapsed = Date.now() - startTime;
                displayUpdate();
            }, 1)
            // console.log('start clicked');
            event.stopPropagation();
        }


        const timerPause = (event) => {
            clearInterval(intervalTimer);
            console.log('pause clicked');
            event.stopPropagation();
            };


        const timerReset = (event) => {
            clearInterval(intervalTimer);
            lapsed = 0;
            displayUpdate();
            casts = [];

            let castDisplay = document.querySelector('.casts');
            castDisplay.textContent = 'None';
        };

        const timerCast = (event) => {
            casts.push(lapsed);
            
            let castIndex = document.querySelector('.casts');
            castDisplay.textContent = `CAST ${castIndex} - ${timeFormat(lapsed)}`;
        }


        let startBtn = document.querySelector('#start');
        startBtn = addEventListener('click', timerStart)


        // let pauseBtn = document.querySelector('#pauseed');
        // pauseBtn = addEventListener('click', timerPause);

        let resetBtn = document.querySelector('#reset');
        resetButton.addEventListener('click', timerReset)

        let castBtn = document.querySelector('#reset');
        resetButton.addEventListener('click', timerCast)


    </script>
</body>
</html>
