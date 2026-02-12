<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Valentine? 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .container {
            background: white;
            border-radius: 30px;
            padding: 40px;
            max-width: 600px;
            width: 100%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            text-align: center;
            position: relative;
        }

        h1 {
            color: #e63946;
            font-size: 2.5em;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .hearts {
            font-size: 2em;
            margin-bottom: 20px;
            animation: pulse 1.5s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .photo-container {
            margin: 30px 0;
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
        }

        .photo-upload {
            width: 100%;
            height: 300px;
            border: 3px dashed #e63946;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: #fff5f7;
        }

        .photo-upload:hover {
            background: #ffe5eb;
            border-color: #d62839;
        }

        .photo-upload p {
            color: #e63946;
            font-size: 1.1em;
            margin-top: 10px;
        }

        .upload-icon {
            font-size: 3em;
            color: #e63946;
        }

        #photoPreview {
            display: none;
            width: 100%;
            height: 300px;
            object-fit: cover;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }

        #photoPreview.show {
            display: block;
        }

        .message {
            font-size: 1.2em;
            color: #2d3748;
            line-height: 1.8;
            margin: 30px 0;
            font-style: italic;
        }

        .question {
            font-size: 1.8em;
            color: #e63946;
            font-weight: bold;
            margin: 30px 0 40px 0;
        }

        .buttons-container {
            position: relative;
            height: 150px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
        }

        button {
            padding: 15px 40px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        #yesBtn {
            background: #e63946;
            color: white;
        }

        #yesBtn:hover {
            background: #d62839;
            transform: scale(1.1);
        }

        #noBtn {
            background: #718096;
            color: white;
            position: absolute;
            transition: all 0.2s ease;
        }

        #noBtn:hover {
            background: #4a5568;
        }

        .celebration {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(230, 57, 70, 0.95);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .celebration.show {
            display: flex;
        }

        .celebration-content {
            text-align: center;
            color: white;
        }

        .celebration-content h2 {
            font-size: 4em;
            margin-bottom: 20px;
            animation: bounce 1s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .celebration-content p {
            font-size: 2em;
        }

        input[type="file"] {
            display: none;
        }

        @media (max-width: 600px) {
            h1 {
                font-size: 2em;
            }
            
            .question {
                font-size: 1.4em;
            }
            
            button {
                padding: 12px 30px;
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="hearts">💕 💝 💖</div>
        <h1>Hey Beautiful!</h1>
        
        <div class="photo-container">
            <label for="photoInput" class="photo-upload" id="uploadArea">
                <span class="upload-icon">📷</span>
                <p>Click to add your favorite photo of us!</p>
            </label>
            <img id="photoPreview" alt="Our photo">
            <input type="file" id="photoInput" accept="image/*">
        </div>

        <div class="message">
            Every moment with you feels like a dream come true. You make my heart skip a beat, 
            my days brighter, and my life infinitely better. I can't imagine celebrating this 
            Valentine's Day with anyone else but you.
        </div>

        <div class="question">
            Will you be my Valentine? 💘
        </div>

        <div class="buttons-container">
            <button id="yesBtn">Yes! 💕</button>
            <button id="noBtn">No</button>
        </div>
    </div>

    <div class="celebration" id="celebration">
        <div class="celebration-content">
            <h2>🎉 YAY! 🎉</h2>
            <p>I knew you'd say yes! ❤️</p>
            <p style="font-size: 1.5em; margin-top: 20px;">Happy Valentine's Day, my love! 💕</p>
        </div>
    </div>

    <script>
        const noBtn = document.getElementById('noBtn');
        const yesBtn = document.getElementById('yesBtn');
        const celebration = document.getElementById('celebration');
        const photoInput = document.getElementById('photoInput');
        const photoPreview = document.getElementById('photoPreview');
        const uploadArea = document.getElementById('uploadArea');
        const buttonsContainer = document.querySelector('.buttons-container');

        // Photo upload functionality
        uploadArea.addEventListener('click', () => {
            photoInput.click();
        });

        photoInput.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    photoPreview.src = e.target.result;
                    photoPreview.classList.add('show');
                    uploadArea.style.display = 'none';
                };
                reader.readAsDataURL(file);
            }
        });

        // Make "No" button run away
        noBtn.addEventListener('mouseover', () => {
            const containerRect = buttonsContainer.getBoundingClientRect();
            const btnRect = noBtn.getBoundingClientRect();
            
            // Calculate random position within container
            const maxX = containerRect.width - btnRect.width;
            const maxY = containerRect.height - btnRect.height;
            
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        });

        // Also move on mobile touch
        noBtn.addEventListener('touchstart', (e) => {
            e.preventDefault();
            const containerRect = buttonsContainer.getBoundingClientRect();
            const btnRect = noBtn.getBoundingClientRect();
            
            const maxX = containerRect.width - btnRect.width;
            const maxY = containerRect.height - btnRect.height;
            
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        });

        // "Yes" button celebration
        yesBtn.addEventListener('click', () => {
            celebration.classList.add('show');
            
            // Create floating hearts
            for (let i = 0; i < 50; i++) {
                createHeart();
            }
        });

        function createHeart() {
            const heart = document.createElement('div');
            heart.innerHTML = '❤️';
            heart.style.position = 'fixed';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.top = '100vh';
            heart.style.fontSize = (Math.random() * 30 + 20) + 'px';
            heart.style.opacity = '0';
            heart.style.transition = 'all 3s ease-in-out';
            heart.style.zIndex = '1001';
            
            document.body.appendChild(heart);
            
            setTimeout(() => {
                heart.style.top = '-100px';
                heart.style.opacity = '1';
                heart.style.transform = `translateX(${(Math.random() - 0.5) * 200}px) rotate(${Math.random() * 360}deg)`;
            }, 100);
            
            setTimeout(() => {
                heart.remove();
            }, 3100);
        }
    </script>
</body>
</html>
