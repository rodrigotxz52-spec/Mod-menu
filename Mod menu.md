<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VIP PANEL | RODRIGO</title>
    <style>
        :root { --primary-red: #ff0000; --bg-black: #050505; }
        body { margin: 0; background: var(--bg-black); color: white; font-family: 'Courier New', Courier, monospace; overflow: hidden; display: flex; justify-content: center; align-items: center; height: 100vh; }
        #matrix-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; opacity: 0.3; }
        .container { background: rgba(10, 10, 10, 0.95); padding: 25px; border-radius: 5px; border: 1px solid var(--primary-red); box-shadow: 0 0 30px rgba(255, 0, 0, 0.4); width: 380px; text-align: center; z-index: 10; }
        h2 { color: var(--primary-red); text-shadow: 0 0 10px var(--primary-red); text-transform: uppercase; letter-spacing: 3px; margin: 10px 0; }
        input { width: 85%; padding: 12px; margin: 8px 0; background: #000; border: 1px solid #400; color: #ff0000; text-align: center; outline: none; font-weight: bold; }
        button { width: 100%; padding: 15px; background: var(--primary-red); color: black; border: none; font-weight: bold; cursor: pointer; text-transform: uppercase; transition: 0.3s; margin-top: 10px; }
        button:hover { background: white; box-shadow: 0 0 20px white; }
        .option-item { display: flex; justify-content: space-between; align-items: center; padding: 8px; border-bottom: 1px solid #200; font-size: 13px; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider { width: 34px; height: 16px; background: #333; display: inline-block; position: relative; cursor: pointer; border-radius: 20px; }
        .slider:before { content: ""; position: absolute; height: 12px; width: 12px; left: 2px; bottom: 2px; background: white; transition: 0.4s; border-radius: 50%; }
        input:checked + .slider { background: var(--primary-red); }
        input:checked + .slider:before { transform: translateX(18px); }
        #panel-container { display: none; }
        .id-status { font-size: 10px; color: #888; margin-top: 5px; height: 15px; }
    </style>
</head>
<body>

    <canvas id="matrix-bg"></canvas>

    <!-- Audios (URLs de exemplo, substitua se desejar) -->
    <audio id="clickSound" src="https://www.soundjay.com"></audio>
    <audio id="bgMusic" loop src="https://www.soundhelix.com"></audio>

    <!-- LOGIN -->
    <div id="login-container" class="container">
        <h2>LOGIN</h2>
        <input type="text" id="user" placeholder="USER">
        <input type="password" id="pass" placeholder="PASSWORD">
        <button onclick="auth()">INJETAR PAINEL</button>
    </div>

    <!-- PAINEL -->
    <div id="panel-container" class="container">
        <h2>RODRIGO VIP</h2>
        
        <div style="margin-bottom: 15px; padding: 10px; border: 1px dashed #400;">
            <input type="text" id="playerID" placeholder="ID DO JOGADOR" style="width: 70%; font-size: 16px;">
            <button onclick="bindID()" style="width: 25%; padding: 10px; margin: 0; font-size: 10px;">VINCULAR</button>
            <div id="idStatus" class="id-status">Aguardando ID...</div>
        </div>

        <div class="option-item"><span>HS PESCOÇO</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>HS PEITO</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>HS CABEÇA</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>HS ACIMA DA CABEÇA</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>FULL HS</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>ANT BAN</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>ANT BLACKLIST</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>80% HS</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <div class="option-item"><span>2X AUTOMÁTICA</span><label class="switch"><input type="checkbox" onchange="playClick()"><span class="slider"></span></label></div>
        <button onclick="location.reload()" style="margin-top:15px; background: #222; color: red;">TERMINAR</button>
    </div>

    <script>
        const clickSound = document.getElementById('clickSound');
        const bgMusic = document.getElementById('bgMusic');

        function playClick() { clickSound.play(); }

        function auth() {
            const u = document.getElementById('user').value;
            const p = document.getElementById('pass').value;
            if (u === "Rodrigo" && p === "xiter") {
                bgMusic.play();
                document.getElementById('login-container').style.display = 'none';
                document.getElementById('panel-container').style.display = 'block';
            } else {
                alert("ACESSO NEGADO");
            }
        }

        function bindID() {
            const id = document.getElementById('playerID').value;
            const status = document.getElementById('idStatus');
            if(id.length > 4) {
                playClick();
                status.innerText = "LOCALIZANDO JOGADOR...";
                status.style.color = "yellow";
                setTimeout(() => {
                    status.innerText = "ID " + id + " VINCULADO COM SUCESSO!";
                    status.style.color = "#00ff00";
                }, 2000);
            } else {
                alert("INSIRA UM ID VÁLIDO!");
            }
        }

        // Matrix Effect
        const canvas = document.getElementById('matrix-bg');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth; canvas.height = window.innerHeight;
        const letters = "010101RODRIGOVIP";
        const fontSize = 16;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);
        function drawMatrix() {
            ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "#ff0000";
            ctx.font = fontSize + "px arial";
            for (let i = 0; i < drops.length; i++) {
                const text = letters.charAt(Math.floor(Math.random() * letters.length));
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
                drops[i]++;
            }
        }
        setInterval(drawMatrix, 50);
    </script>
</body>
</html>
