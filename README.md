<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>VFD Pro</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');
        
        * { box-sizing: border-box; touch-action: manipulation; }
        
        body, html { 
            background-color: #050505; 
            height: 100vh; 
            width: 100vw; 
            margin: 0; 
            padding: 0;
            font-family: 'Share Tech Mono', monospace; 
            overflow: hidden; 
        }

        /* This wrapper occupies the whole screen and pushes content down */
        .main-wrapper {
            display: flex;
            flex-direction: column;
            height: 100vh;
            justify-content: flex-end; /* Pushes everything to the bottom */
        }

        /* The VFD Screen area */
        .display-unit {
            background: #010808;
            border-top: 1px solid #1a1a1a;
            position: relative;
            /* Control how much of the top screen you see */
            height: 40vh; 
            display: flex;
            flex-direction: column;
        }

        .display-unit::after { 
            content: ""; position: absolute; top: 0; left: 0; width: 100%; height: 100%; 
            background-image: radial-gradient(circle, transparent 20%, rgba(0,0,0,0.7) 70%); 
            background-size: 2px 2px; pointer-events: none; 
        }

        .history-viewport { flex-grow: 1; overflow-y: auto; padding: 10px; display: flex; flex-direction: column; }
        #history-container { margin-top: auto; }
        .history-item { color: #26bf9e; display: flex; flex-direction: column; padding: 5px 10px; }
        .history-item span:last-child { align-self: flex-end; color: #33ffcc; font-weight: bold; }

        .divider { height: 3px; background: #33ffcc; box-shadow: 0 0 10px #33ffcc; margin: 5px 0; flex-shrink: 0; }
        
        .current-line { 
            color: #33ffcc; font-size: 3rem; font-weight: bold; 
            text-align: right; padding: 0 15px; min-height: 4.5rem; 
            display: flex; align-items: center; justify-content: flex-end;
        }

        /* The Physical Keyboard */
        .keyboard-unit {
            background: #0a0a0a;
            height: 50vh; /* Fixed height for the keys */
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 6px;
            padding: 10px;
            /* Adds safe area for modern phones */
            padding-bottom: calc(10px + env(safe-area-inset-bottom));
        }

        button {
            background: linear-gradient(145deg, #222, #111);
            color: #ccc; border: 1px solid #000; border-radius: 4px;
            font-family: 'Share Tech Mono', monospace; font-size: 1.2rem;
            display: flex; align-items: center; justify-content: center;
        }

        button:active { background: #444; }
        .nav-btn { color: #33ffcc; background: #181818; }
        .eq { background: #003328; color: #33ffcc; }
        .shift-btn { background: #f5a623 !important; color: #fff !important; }
        .ac { background: #330000; color: #ff9999; }
    </style>
</head>
<body>

    <div class="main-wrapper">
        <div class="display-unit">
            <div class="history-viewport"><div id="history-container"></div></div>
            <div class="divider"></div>
            <div id="input-line-container" class="current-line"></div>
        </div>

        <div class="keyboard-unit" id="main-grid">
            <button class="shift-btn" data-val="shift">SHIFT</button>
            <button class="nav-btn" data-val="left">◀</button>
            <button class="nav-btn" data-val="right">▶</button>
            <button class="ac" data-val="ac">CLR</button>
            <button class="nav-btn" data-val="up">▲</button>
            <button data-val="exp">e<sup>x</sup></button>
            <button data-val="π">π</button>
            <button data-val="del">⌫</button>
            <button class="nav-btn" data-val="down">▼</button>
            <button data-val="(">(</button>
            <button data-val=")">)</button>
            <button data-val="^">^</button>
            <button data-val="sin">SIN</button>
            <button data-val="cos">COS</button>
            <button data-val="tan">TAN</button>
            <button data-val="/">÷</button>
            <button data-val="7">7</button><button data-val="8">8</button><button data-val="9">9</button><button data-val="*">×</button>
            <button data-val="4">4</button><button data-val="5">5</button><button data-val="6">6</button><button data-val="-">-</button>
            <button data-val="1">1</button><button data-val="2">2</button><button data-val="3">3</button><button data-val="+">+</button>
            <button data-val="0">0</button>
            <button data-val=".">.</button>
            <button data-val="ans">ANS</button>
            <button class="eq" data-val="=">EXE</button>
        </div>
    </div>

    <script>
        // Use the same logic as before
        let entryArr = [];
        const inputDisplay = document.getElementById('input-line-container');

        document.getElementById('main-grid').addEventListener('pointerdown', (e) => {
            const btn = e.target.closest('button');
            if (!btn) return;
            const val = btn.getAttribute('data-val');
            
            if (val === 'ac') entryArr = [];
            else if (val === 'del') entryArr.pop();
            else if (val !== '=' && val !== 'shift') entryArr.push(val);
            
            inputDisplay.innerText = entryArr.join('');
        });
    </script>
</body>
</html>
