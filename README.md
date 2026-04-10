<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Для тебя ❤️</title>

<style>
body {
    margin: 0;
    height: 100vh;
    background: radial-gradient(circle at center, #1a0026, #000);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    font-family: Arial, sans-serif;
    overflow: hidden;
    padding: 20px;
}

/* ТЕКСТ */
h1 {
    color: #ff4dff;
    text-align: center;
    font-size: 28px;
    text-shadow: 0 0 10px #ff00ff;
}

/* КНОПКИ */
button {
    width: 80%;
    max-width: 320px;
    padding: 18px;
    margin: 10px;
    font-size: 18px;
    border: none;
    border-radius: 14px;
    cursor: pointer;
}

/* ДА */
#yes {
    background: #00ff99;
}

/* НЕТ */
#no {
    position: fixed;
    background: #ff0066;
    color: white;
}

/* СПИСОК */
.list {
    width: 100%;
    max-width: 500px;
}

.list button {
    width: 100%;
    text-align: left;
    background: #111;
    color: white;
    border: 1px solid #ff00ff;
    font-size: 16px;
}
</style>
</head>

<body>

<h1 id="title">Пойдешь со мной на свидание? 💖</h1>

<button id="yes">ДА</button>
<button id="no">НЕТ</button>

<script>
const noBtn = document.getElementById("no");

/* 📱 ДЛЯ ПАЛЬЦА (touch) */
document.addEventListener("touchstart", moveButton);
document.addEventListener("mousemove", moveButton);

function moveButton(e) {
    let x, y;

    if (e.touches) {
        x = e.touches[0].clientX;
        y = e.touches[0].clientY;
    } else {
        x = e.clientX;
        y = e.clientY;
    }

    const offset = 100;

    const newX = x + (Math.random() * offset - offset/2);
    const newY = y + (Math.random() * offset - offset/2);

    noBtn.style.left = newX + "px";
    noBtn.style.top = newY + "px";
}

/* ДА → СТРАНИЦА ВЫБОРА */
document.getElementById("yes").onclick = () => {

    document.body.innerHTML = `
    <h1>Выбирай свидание 💫</h1>
    <div class="list" id="dates"></div>
    `;

    const ideas = [
        "1. Чтение друг другу книг вслух, с эмоциями, как актеры.",
        "2. Пешеходная прогулка до рассвета, чтобы встретить солнце вдвоем.",
        "3. Поиск созвездий и выдумывание собственных легенд о них.",
        "4. Совместный рисунок на старой простыне или большом ватмане.",
        "5. Съемка друг друга на камеру, как будто это кино.",
        "6. Спонтанное интервью друг с другом — будто вы знаменитости.",
        "7. Сидеть в людном месте и придумывать истории случайных прохожих.",
        "8. Хочу окультуриваться (музей, театры и т.д)."
    ];

    const container = document.getElementById("dates");

    ideas.forEach((text, index) => {
        const btn = document.createElement("button");
        btn.innerText = text;

        btn.onclick = () => {
            document.body.innerHTML = `
            <h1>🔥 Отличный выбор!</h1>
            <button onclick="sendMessage(${index + 1})">
                Напиши мне число, время и номер свидания
            </button>
            `;
        };

        container.appendChild(btn);
    });
};

/* 📩 ОТПРАВКА */
function sendMessage(num) {
    const text = encodeURIComponent(
        "Я выбираю свидание №" + num + " 💖 Давай обсудим время 😏"
    );

    /* сюда вставь свой телеграм или whatsapp */
    window.location.href = "https://t.me/ВАШ_НИК?text=" + text;

    // альтернатива:
    // window.location.href = "https://wa.me/XXXXXXXXXXX?text=" + text;
}
</script>

</body>
</html>
