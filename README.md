<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>All-in-one Video Downloader</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Orbitron', sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: white;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0;
            overflow: hidden;
            position: relative;
            transition: background 1s ease-in-out;
        }

        .container {
            background: rgba(0, 0, 0, 0.8);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            text-align: center;
            position: relative;
            z-index: 1; /* Ensure it is above the neon background */
            animation: fadeIn 1.5s ease-in-out;
        }

        h1 {
            margin-bottom: 20px;
            font-size: 2.5rem;
            letter-spacing: 2px;
            text-shadow: 0 0 5px #fff, 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 40px #ff00ff, 0 0 80px #ff00ff, 0 0 90px #ff00ff, 0 0 100px #ff00ff, 0 0 150px #ff00ff;
            animation: neon 1.5s ease-in-out infinite alternate;
        }

        form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        input, select, button {
            margin: 10px 0;
            padding: 15px;
            width: 100%;
            max-width: 400px;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
        }

        input, select {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            transition: background 0.3s ease-in-out, color 0.3s ease-in-out;
            text-shadow: 0 0 5px #fff, 0 0 10px #00bfff, 0 0 20px #00bfff, 0 0 40px #00bfff, 0 0 80px #00bfff, 0 0 90px #00bfff, 0 0 100px #00bfff, 0 0 150px #00bfff;
        }

        input:focus, select:focus {
            background: rgba(255, 255, 255, 0.2);
            outline: none;
        }

        button {
            background: linear-gradient(45deg, #ff416c, #ff4b2b);
            color: white;
            cursor: pointer;
            transition: transform 0.2s, background 0.3s ease-in-out;
            text-shadow: 0 0 5px #fff, 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 40px #ff00ff, 0 0 80px #ff00ff, 0 0 90px #ff00ff, 0 0 100px #ff00ff, 0 0 150px #ff00ff;
        }

        button:hover {
            transform: scale(1.05);
            background: linear-gradient(45deg, #ff4b2b, #ff416c);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes neon {
            from {
                text-shadow: 0 0 5px #fff, 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 40px #ff00ff, 0 0 80px #ff00ff, 0 0 90px #ff00ff, 0 0 100px #ff00ff, 0 0 150px #ff00ff;
            }
            to {
                text-shadow: 0 0 10px #fff, 0 0 20px #ff00ff, 0 0 30px #ff00ff, 0 0 50px #ff00ff, 0 0 100px #ff00ff, 0 0 110px #ff00ff, 0 0 120px #ff00ff, 0 0 150px #ff00ff;
            }
        }

        @keyframes blueGreenLights {
            0% {
                background: radial-gradient(circle, rgba(0, 255, 255, 0.5) 0%, rgba(0, 255, 255, 0) 70%), radial-gradient(circle, rgba(0, 255, 0, 0.5) 0%, rgba(0, 255, 0, 0) 70%);
            }
            50% {
                background: radial-gradient(circle, rgba(0, 255, 255, 0.5) 0%, rgba(0, 255, 255, 0) 70%), radial-gradient(circle, rgba(0, 255, 0, 0) 0%, rgba(0, 255, 0, 0.5) 70%);
            }
            100% {
                background: radial-gradient(circle, rgba(0, 255, 255, 0) 0%, rgba(0, 255, 255, 0.5) 70%), radial-gradient(circle, rgba(0, 255, 0, 0.5) 0%, rgba(0, 255, 0, 0) 70%);
            }
        }

        .neon-background {
            animation: blueGreenLights 2s infinite alternate;
        }

        .loading {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 1.5rem;
            text-align: center;
            z-index: 1000;
            color: white;
        }

        .loading span {
            display: inline-block;
            margin: 0 5px;
            animation: loading 1.5s infinite;
        }

        .loading span:nth-child(1) {
            animation-delay: 0s;
        }

        .loading span:nth-child(2) {
            animation-delay: 0.3s;
        }

        .loading span:nth-child(3) {
            animation-delay: 0.6s;
        }

        @keyframes loading {
            0%, 80%, 100% {
                transform: scale(1);
            }
            40% {
                transform: scale(1.5);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>All-in-one Video Downloader</h1>
        <form action="/download" method="post">
            <input type="text" name="url" placeholder="Enter video URL" required>
            <select name="platform" required>
                <option value="" disabled selected>Select Platform</option>
                <option value="youtube">YouTube</option>
                <option value="instagram">Instagram</option>
                <option value="facebook">Facebook</option>
                <option value="tiktok">TikTok</option> <!-- Added TikTok option -->
            </select>
            <button type="submit">Download</button>
        </form>
    </div>
    <div class="loading">
        <span>.</span><span>.</span><span>.</span>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const form = document.querySelector('form');
            const loading = document.querySelector('.loading');
            const body = document.body;

            form.addEventListener('submit', function () {
                body.classList.add('neon-background');
                loading.style.display = 'block';
            });
        });
    </script>

</body>
</html>
