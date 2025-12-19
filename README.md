<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trust Me - Instant</title>
    <style>
        body, html {
            height: 100%;
            margin: 0;
            background-color: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            font-family: sans-serif;
        }

        #trust-button {
            padding: 20px 50px;
            font-size: 24px;
            color: white;
            background-color: #ff0000;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            z-index: 100;
        }

        /* O container do vídeo fica invisível inicialmente */
        #video-wrapper {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            visibility: hidden; 
            opacity: 0;
            transition: opacity 0.5s;
        }

        iframe {
            width: 100vw;
            height: 100vh;
            pointer-events: none; /* Impede que o usuário pause clicando no vídeo */
        }
    </style>
</head>
<body>

    <button id="trust-button">Trust me</button>

    <div id="video-wrapper">
        <div id="player"></div>
    </div>

    <script>
        var player;
        
        // 1. Carrega a API do YouTube de forma assíncrona
        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

        // 2. Cria o player assim que a API estiver pronta
        function onYouTubeIframeAPIReady() {
            player = new YT.Player('player', {
                videoId: 'qnaGs3qlnAs',
                playerVars: {
                    'autoplay': 1,
                    'controls': 0,
                    'mute': 1, // Pré-carrega mudo para permitir autoplay
                    'rel': 0,
                    'modestbranding': 1,
                    'iv_load_policy': 3
                },
                events: {
                    'onReady': onPlayerReady
                }
            });
        }

        function onPlayerReady(event) {
            console.log("Vídeo pré-carregado e pronto!");
        }

        // 3. Ação ao clicar no botão
        document.getElementById('trust-button').addEventListener('click', function() {
            // Remove o botão
            this.style.display = 'none';

            // Faz o vídeo aparecer
            const wrapper = document.getElementById('video-wrapper');
            wrapper.style.visibility = 'visible';
            wrapper.style.opacity = '1';

            // Tira do mudo, reinicia e dá play
            player.unMute();
            player.seekTo(0);
            player.playVideo();

            // Ativa tela cheia do navegador
            const docEl = document.documentElement;
            if (docEl.requestFullscreen) docEl.requestFullscreen();
            else if (docEl.webkitRequestFullscreen) docEl.webkitRequestFullscreen();
        });
    </script>
</body>
</html>
