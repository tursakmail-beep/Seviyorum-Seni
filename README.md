<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seviyorum Seni</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
            font-family: Arial, sans-serif;
            overflow: hidden;
        }

        .heart-container {
            position: relative;
            text-align: center;
        }

        .fa-heart {
            color: #ff4757;
            font-size: 200px;
            animation: pulse 1.5s ease-in-out infinite;
            transition: transform 0.3s ease;
        }

        .fa-heart:hover {
            transform: scale(1.2);
            animation-duration: 0.8s;
        }

        @keyframes pulse {
            0% {
                transform: scale(1);
                opacity: 0.8;
            }
            50% {
                transform: scale(1.3);
                opacity: 1;
            }
            100% {
                transform: scale(1);
                opacity: 0.8;
            }
        }

        .text {
            font-size: 48px;
            color: #ff4757;
            font-weight: bold;
            opacity: 0;
            animation: fadeInOut 1.5s ease-in-out infinite;
            margin-top: 10px; /* Kalbin altına hafif boşluk */
        }

        @keyframes fadeInOut {
            0% { opacity: 0; }
            50% { opacity: 1; }
            100% { opacity: 0; }
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #ff4757;
            border-radius: 50%;
            pointer-events: none;
            animation: float 3s linear infinite;
        }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="heart-container" id="heartContainer">
        <i class="fas fa-heart" id="heart"></i>
        <div class="text" id="loveText">Seni Seviyorum ❤️</div>
    </div>

    <script>
        const heartContainer = document.getElementById('heartContainer');
        const heart = document.getElementById('heart');

        heartContainer.addEventListener('mouseenter', () => {
            heart.style.animationDuration = '0.8s';
        });

        heartContainer.addEventListener('mouseleave', () => {
            heart.style.animationDuration = '1.5s';
        });

        heartContainer.addEventListener('click', (e) => {
            createParticles(e.clientX, e.clientY);
        });

        function createParticles(x, y) {
            for (let i = 0; i < 10; i++) {
                setTimeout(() => {
                    const particle = document.createElement('div');
                    particle.classList.add('particle');
                    particle.style.left = x + (Math.random() - 0.5) * 100 + 'px';
                    particle.style.top = y + (Math.random() - 0.5) * 100 + 'px';
                    particle.style.animationDelay = Math.random() * 0.5 + 's';
                    document.body.appendChild(particle);

                    setTimeout(() => {
                        particle.remove();
                    }, 3000);
                }, i * 100);
            }
        }

        setInterval(() => {
            const rect = heartContainer.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;
            createParticles(centerX, centerY);
        }, 5000);
    </script>
</body>
</html>
