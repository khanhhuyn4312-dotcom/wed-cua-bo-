# wed-cua-bo-
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chúc Mừng Ngày 20/10 ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Quicksand:wght@500;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            height: 100vh;
            width: 100vw;
            background: radial-gradient(circle, #ffb6c1, #ff69b4, #db7093);
            overflow: hidden;
            font-family: 'Quicksand', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* Hiệu ứng trái tim bay background */
        .bg-heart {
            position: absolute;
            color: rgba(255, 255, 255, 0.6);
            animation: floatUp linear infinite;
            z-index: 1;
            pointer-events: none;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0.5) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-10vh) scale(1.2) rotate(360deg); opacity: 0; }
        }

        /* Hộp quà ban đầu */
        .gift-box-container {
            text-align: center;
            z-index: 10;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .gift-box-container:hover {
            transform: scale(1.08);
        }

        .gift-box {
            font-size: 100px;
            animation: pulse 1.2s infinite ease-in-out;
            filter: drop-shadow(0 10px 15px rgba(0,0,0,0.2));
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1) rotate(0deg); }
            25% { transform: scale(1.1) rotate(-5deg); }
            75% { transform: scale(1.1) rotate(5deg); }
        }

        .click-hint {
            margin-top: 15px;
            color: white;
            font-size: 20px;
            font-weight: bold;
            text-shadow: 0 2px 5px rgba(0,0,0,0.3);
            animation: blink 1.5s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }

        /* Thư chứa nội dung */
        .letter-card {
            display: none;
            width: 90%;
            max-width: 500px;
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(10px);
            border-radius: 25px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.25);
            text-align: center;
            z-index: 10;
            border: 3px solid #fff;
            animation: zoomIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes zoomIn {
            from { opacity: 0; transform: scale(0.3); }
            to { opacity: 1; transform: scale(1); }
        }

        .title {
            font-family: 'Dancing Script', cursive;
            font-size: 38px;
            color: #d63384;
            margin-bottom: 15px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }

        .cute-img {
            width: 130px;
            height: 130px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid #ff69b4;
            margin-bottom: 15px;
            box-shadow: 0 5px 15px rgba(255, 105, 180, 0.4);
        }

        .message {
            font-size: 17px;
            color: #444;
            line-height: 1.7;
            min-height: 120px;
            text-align: left;
            margin-bottom: 20px;
            font-weight: 500;
        }

        .heart-btn {
            background: linear-gradient(45deg, #ff416c, #ff4b2b);
            color: white;
            border: none;
            padding: 12px 28px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 65, 108, 0.4);
            transition: all 0.3s ease;
        }

        .heart-btn:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 8px 20px rgba(255, 65, 108, 0.6);
        }

        /* Nhạc nền ẩn */
        audio { display: none; }
    </style>
</head>
<body>

    <!-- Hộp quà ban đầu -->
    <div class="gift-box-container" id="giftBox" onclick="openGift()">
        <div class="gift-box">🎁</div>
        <div class="click-hint">✨ Nhấn vào đây để mở quà 20/10 ✨</div>
    </div>

    <!-- Bức thư chúc mừng -->
    <div class="letter-card" id="letterCard">
        <div class="title">Happy Vietnamese Women's Day!</div>
        <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExdWpvd3Y1ZHk0ZHdma2FqOHBzYnlxdzBmOHZxdms0OHBzOHZxdms0OCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/Lq0h93752f6J9tijrh/giphy.gif" alt="Cute Bunny" class="cute-img">
        <div class="message" id="typedText"></div>
        <button class="heart-btn" onclick="surpriseMore()">Bắn Tim & Hoa 💖</button>
    </div>

    <!-- Nhạc nền ngọt ngào -->
    <audio id="bgMusic" loop src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=lofi-study-112191.mp3"></audio>

    <script>
        // Tạo hiệu ứng trái tim bay liên tục trên nền
        function createBgHearts() {
            const hearts = ['❤️', '💖', '🌸', '✨', '💕', '🌷'];
            setInterval(() => {
                const heart = document.createElement('div');
                heart.classList.add('bg-heart');
                heart.innerText = hearts[Math.floor(Math.random() * hearts.length)];
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
                heart.style.fontSize = (Math.random() * 15 + 15) + 'px';
                document.body.appendChild(heart);

                setTimeout(() => { heart.remove(); }, 7000);
            }, 300);
        }
        createBgHearts();

        // Nội dung lời chúc
        const fullMessage = "Nhân ngày 20/10, chúc bạn/cậu luôn luôn xinh đẹp, rạng rỡ, ngập tràn hạnh phúc và sự yêu thương! Mong rằng mỗi ngày trôi qua đều là những khoảnh khắc tuyệt vời nhất đối với bạn. Cảm ơn vì đã luôn xuất hiện và mang lại sự dịu dàng cho thế giới này! ❤️✨";
        
        let index = 0;

        // Hàm mở quà
        function openGift() {
            // Ẩn hộp quà, hiện thư
            document.getElementById('giftBox').style.display = 'none';
            document.getElementById('letterCard').style.display = 'block';

            // Phát nhạc
            const music = document.getElementById('bgMusic');
            music.play().catch(e => console.log("Cần tương tác người dùng để phát âm thanh"));

            // Pháo hoa trái tim
            fireConfetti();

            // Chạy chữ typewriter
            typeWriter();
        }

        // Hiệu ứng gõ chữ
        function typeWriter() {
            if (index < fullMessage.length) {
                document.getElementById("typedText").innerHTML += fullMessage.charAt(index);
                index++;
                setTimeout(typeWriter, 40);
            }
        }

        // Bắn pháo hoa Confetti
        function fireConfetti() {
            const count = 200;
            const defaults = { origin: { y: 0.7 } };

            function fire(particleRatio, opts) {
                confetti(Object.assign({}, defaults, opts, {
                    particleCount: Math.floor(count * particleRatio)
                }));
            }

            fire(0.25, { spread: 26, startVelocity: 55, colors: ['#ff69b4', '#ff1493'] });
            fire(0.2, { spread: 60, colors: ['#ffffff', '#ffb6c1'] });
            fire(0.35, { spread: 100, decay: 0.91, scalar: 0.8 });
            fire(0.1, { spread: 120, startVelocity: 25, decay: 0.92, scalar: 1.2 });
        }

        // Bấm nút tạo thêm bất ngờ
        function surpriseMore() {
            fireConfetti();
        }
    </script>
</body>
</html>
