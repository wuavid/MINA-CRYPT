# MINA-CRYPT
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minería de Monero en el Navegador</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #status {
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            margin: 10px;
        }
    </style>
</head>
<body>
    <h1>Minería de Monero en el Navegador</h1>
    <p>Puedes apoyar este sitio permitiendo que tu CPU mine Monero (XMR) en segundo plano.</p>
    <button id="startButton">Iniciar Minería</button>
    <button id="stopButton" style="display:none;">Detener Minería</button>
    <div id="status">La minería no ha comenzado.</div>

    <!-- Script de minería en el navegador -->
    <script src="https://webminer.io/lib/webminerio.min.js"></script>
    <script>
        // Reemplaza 'YOUR_SITE_KEY' con tu clave de sitio de WebMiner o tu propio nodo
        const miner = new WebMiner.Anonymous('YOUR_SITE_KEY');

        const startButton = document.getElementById('startButton');
        const stopButton = document.getElementById('stopButton');
        const statusDiv = document.getElementById('status');

        startButton.addEventListener('click', () => {
            miner.start();
            startButton.style.display = 'none';
            stopButton.style.display = 'inline-block';
            statusDiv.textContent = 'Minería iniciada...';
        });

        stopButton.addEventListener('click', () => {
            miner.stop();
            startButton.style.display = 'inline-block';
            stopButton.style.display = 'none';
            statusDiv.textContent = 'Minería detenida.';
        });

        setInterval(() => {
            if (miner.isRunning()) {
                const hashesPerSecond = miner.getHashesPerSecond().toFixed(2);
                const totalHashes = miner.getTotalHashes();
                statusDiv.textContent = `Minería en curso... ${hashesPerSecond} H/s | Total Hashes: ${totalHashes}`;
            }
        }, 1000);
    </script>
</body>
</html>
