<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Romantic Letter</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        textarea { width: 80%; height: 150px; margin: 10px 0; }
        .hidden { display: none; }
        .container { max-width: 600px; margin: auto; }
        .letter { white-space: pre-wrap; background: #ffe4e1; padding: 20px; border-radius: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Write Your Romantic Letter</h2>
        <textarea id="letterInput" placeholder="Write your message here..."></textarea>
        <br>
        <button onclick="generateLink()">Generate Shareable Link</button>
        <p id="linkContainer" class="hidden">Share this link: <a id="generatedLink" href="#"></a></p>
        
        <div id="letterDisplay" class="hidden">
            <h2>Your Received Letter</h2>
            <p class="letter" id="letterText"></p>
        </div>
    </div>
    
    <script>
        function generateLink() {
            const letter = encodeURIComponent(document.getElementById('letterInput').value);
            const url = window.location.origin + window.location.pathname + "?letter=" + letter;
            document.getElementById('generatedLink').href = url;
            document.getElementById('generatedLink').textContent = url;
            document.getElementById('linkContainer').classList.remove('hidden');
        }
        
        function displayLetter() {
            const params = new URLSearchParams(window.location.search);
            if (params.has('letter')) {
                document.getElementById('letterText').textContent = decodeURIComponent(params.get('letter'));
                document.getElementById('letterDisplay').classList.remove('hidden');
                document.querySelector('.container h2').classList.add('hidden');
                document.querySelector('textarea').classList.add('hidden');
                document.querySelector('button').classList.add('hidden');
            }
        }
        
        window.onload = displayLetter;
    </script>
</body>
</html>
