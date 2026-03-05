<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Device Security Check</title>
    <style>
        body { background: #0b0e14; color: white; font-family: sans-serif; text-align: center; padding-top: 50px; }
        .box { background: #161b22; margin: auto; padding: 20px; width: 80%; border-radius: 15px; }
        .status { font-weight: bold; margin-top: 20px; font-size: 1.2em; }
        .loader { border: 4px solid #f3f3f3; border-top: 4px solid #3d5afe; border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; margin: 20px auto; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body>

<div class="box">
    <h2>Security Analysis</h2>
    <div id="loader" class="loader"></div>
    <div id="msg">Scanning your device hardware...</div>
    <div id="status" class="status"></div>
</div>

<script>
    function getFingerprint() {
        // Device ki unique details nikalna
        const canvas = document.createElement('canvas');
        const gl = canvas.getContext('webgl');
        const debugInfo = gl.getExtension('WEBGL_debug_renderer_info');
        const renderer = gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL);
        return btoa(navigator.userAgent + renderer + screen.width + screen.height);
    }

    setTimeout(() => {
        const fingerPrint = getFingerprint();
        document.getElementById('loader').style.display = 'none';
        
        // Telegram Bot ko redirect karna fingerprint ke saath
        // Apne bot ka username yahan badlein
        window.location.href = "https://t.me/YOUR_BOT_USERNAME?start=check_" + fingerPrint;
    }, 3000);
</script>

</body>
</html>
