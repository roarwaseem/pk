<!DOCTYPE html>
<html lang="ur" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Urdu Notebook Customizer</title>
    
    <!-- Jameel Noori Font -->
    <link href="https://fonts.cdnfonts.com/css/jameel-noori-nastaleeq" rel="stylesheet">
    
    <style>
        * { box-sizing: border-box; }

        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            transition: background-color 0.3s ease;
        }

        /* Notebook Style */
        .notebook-container {
            width: 100%;
            min-height: 100vh;
            padding: 50px 80px;
            /* Default Paper Style */
            background-image: linear-gradient(rgba(0,0,0,0.05) 1px, transparent 1px);
            background-size: 100% 45px;
            position: relative;
        }

        /* Red Margin Line */
        .notebook-container::before {
            content: '';
            position: absolute;
            top: 0;
            right: 60px;
            width: 2px;
            height: 100%;
            background-color: rgba(255, 0, 0, 0.2);
        }

        #urduEditor {
            width: 100%;
            min-height: 85vh;
            background: transparent;
            border: none;
            outline: none;
            font-family: 'Jameel Noori Nastaleeq', serif;
            font-size: 30px;
            line-height: 45px;
            color: #333; /* Default Color */
            resize: none;
            display: block;
        }

        /* Top Settings Bar */
        .settings-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: #fff;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            z-index: 1000;
            direction: ltr; /* Buttons left to right hi ache lagte hain */
        }

        .control-group {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 14px;
            font-family: sans-serif;
        }

        input[type="color"] {
            border: none;
            width: 30px;
            height: 30px;
            cursor: pointer;
            background: none;
        }

        button {
            padding: 6px 12px;
            cursor: pointer;
            border: 1px solid #ddd;
            background: white;
            border-radius: 4px;
        }

        button:hover { background: #f9f9f9; }

        @media print { .settings-bar { display: none; } }
    </style>
</head>
<body id="mainBody" style="background-color: #fdfcf0;">

    <div class="settings-bar">
        <div class="control-group">
            <span>Page:</span>
            <input type="color" id="bgColorPicker" value="#fdfcf0" oninput="changeBgColor(this.value)">
        </div>
        <div class="control-group">
            <span>Font:</span>
            <input type="color" id="fontColorPicker" value="#333333" oninput="changeFontColor(this.value)">
        </div>
        <button onclick="toggleFullScreen()">Full Screen</button>
        <button onclick="copyText()">Copy</button>
        <button style="color: red;" onclick="clearAll()">Clear</button>
    </div>

    <div class="notebook-container">
        <textarea 
            id="urduEditor" 
            placeholder="Yahan Urdu likhein..."
            oninput="autoResize(this)"></textarea>
    </div>

    <script>
        function changeBgColor(color) {
            document.getElementById("mainBody").style.backgroundColor = color;
        }

        function changeFontColor(color) {
            document.getElementById("urduEditor").style.color = color;
        }

        function autoResize(textarea) {
            textarea.style.height = 'auto';
            textarea.style.height = textarea.scrollHeight + 'px';
        }

        function copyText() {
            const text = document.getElementById("urduEditor");
            text.select();
            document.execCommand("copy");
            alert("Copy ho gaya!");
        }

        function clearAll() {
            if(confirm("Sab mita dein?")) {
                document.getElementById("urduEditor").value = "";
            }
        }

        function toggleFullScreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen();
            } else {
                document.exitFullscreen();
            }
        }
    </script>

</body>
</html>
