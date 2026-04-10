<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Для тебя ❤️</title>

    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            font-family: Arial, sans-serif;
            overflow: hidden;
        }

        h1 {
            font-size: 48px;
            color: white;
            text-align: center;
            margin-bottom: 40px;
        }

        .buttons {
            position: relative;
        }

        button {
            font-size: 20px;
            padding: 15px 30px;
            margin: 10px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: 0.2s;
        }

        #yes {
            background-color: #4CAF50;
            color: white;
        }

        #yes:hover {
            transform: scale(1.1);
        }

        #no {
            background-color: #f44336;
            color: white;
            position: absolute;
        }
    </style>
</head>

<body>

    <h1>Пойдешь со мной на свидание? 💖</h1>

    <div class="buttons">
        <button id="yes">ДА</button>
        <button id="no">НЕТ</button>
    </div>

    <script>
        const noBtn = document.getElementById("no");

        noBtn.addEventListener("mouseover", () => {
            const x = Math.random() * (window.innerWidth - 100);
            const y = Math.random() * (window.innerHeight - 50);

            noBtn.style.left = x + "px";
            noBtn.style.top = y + "px";
        });

        document.getElementById("yes").addEventListener("click", () => {
            document.body.innerHTML = "<h1>Я знал 😍❤️</h1>";
        });
    </script>

</body>
</html>
