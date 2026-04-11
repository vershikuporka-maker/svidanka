<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap" rel="stylesheet">

<title>Для тебя ❤️</title>

<style>
body {
    margin: 0;
    height: 100vh;
    font-family: 'Comic Neue', cursive;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow: hidden;

    /* КАРАНДАШНЫЙ ФОН */
    background: repeating-linear-gradient(
        45deg,
        #f5f5f5,
        #f5f5f5 10px,
        #eeeeee 10px,
        #eeeeee 20px
    );
}

/* ЗАГОЛОВОК */
.title {
    font-size: 26px;
    text-align: center;
    padding: 20px;
    border: 3px solid #000;
    border-radius: 20px;
    background: #fff;
    box-shadow: 4px 4px 0 #000;
    position: relative;
}

/* КОТ НА ЗАГОЛОВКЕ */
.cat-top {
    position: absolute;
    top: -30px;
    right: 10px;
    font-size: 30px;
}

/* КНОПКИ — КАК НАРИСОВАНЫ */
button {
    margin: 10px;
    padding: 15px 20px;
    font-size: 18px;
    border-radius: 20px;
    border: 3px solid black;
    background: #fff;
    box-shadow: 3px 3px 0 black;
    cursor: pointer;
    transition: 0.1s;
}

button:active {
    transform: translate(2px,2px);
    box-shadow: 1px 1px 0 black;
}

#yes {
    background: #baffc9;
}

#no {
    background: #ffb3ba;
}

/* СПИСОК */
.list {
    width: 90%;
    max-width: 500px;
}

/* КОТИКИ */
.cat {
    position: absolute;
    font-size: 24px;
    cursor: pointer;
    transition: 0.2s;
}

.cat:active {
    transform: scale(1.5) rotate(10deg);
}

/* СЕРДЕЧКИ */
.heart {
    position: absolute;
    color: red;
    animation: float 1s ease-out forwards;
}

@keyframes float {
    0% { opacity:1; transform: translateY(0); }
    100% { opacity:0; transform: translateY(-80px); }
}
</style>
</head>

<body>

<div class="title">
    Пойдешь со мной на свидание? 💖
    <div class="cat-top">🐱</div>
</div>

<button id="yes">ДА</button>
<button id="no">НЕТ</button>

<!-- КОТИКИ -->
<div class="cat" style="top:20%; left:10%">🐈</div>
<div class="cat" style="top:60%; left:70%">🐈‍⬛</div>

<script>
const noBtn = document.getElementById("no");

/* НЕТ УМЕНЬШАЕТСЯ */
noBtn.onclick = () => {
    noBtn.style.transform = "scale(0.2)";
};

/* СЕРДЕЧКИ ПРИ КЛИКЕ */
document.addEventListener("click", (e) => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerText = "💖";

    heart.style.left = e.clientX + "px";
    heart.style.top = e.clientY + "px";

    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 1000);
});

/* КОТИКИ РЕАГИРУЮТ */
document.querySelectorAll(".cat").forEach(cat => {
    cat.addEventListener("click", () => {
        cat.innerText = "😻";
        setTimeout(() => cat.innerText = "🐱", 500);
    });
});

/* ДА → СТРАНИЦА */
document.getElementById("yes").onclick = () => {
document.getElementById("yes").onclick = () => {

    document.body.innerHTML = `
    <div class="page">
        <div class="title">Выбирай свидание 💫</div>
        <div class="list" id="dates"></div>
    </div>
    `;

    /* ДОБАВЛЯЕМ СТИЛИ ТАКИЕ ЖЕ КАК НА 1 СТРАНИЦЕ */
    const style = document.createElement("style");
    style.innerHTML = `
    .page {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        width: 100%;
    }

    .list {
        width: 90%;
        max-width: 420px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .list button {
        width: 100%;
        margin: 8px 0;
    }
    `;
    document.head.appendChild(style);

    const ideas = [
        "1. Чтение друг другу книг вслух, с эмоциями, как актеры.",
        "2. Пешеходная прогулка до рассвета, чтобы встретить солнце вдвоем.",
        "3. Поиск созвездий и выдумывание легенд.",
        "4. Совместный рисунок.",
        "5. Съемка как кино.",
        "6. Интервью как знаменитости.",
        "7. Придумывать истории прохожим.",
        "8. Музей / театр."
    ];

    const container = document.getElementById("dates");

    ideas.forEach((text, index) => {
        const btn = document.createElement("button");
        btn.innerText = text;

        btn.onclick = () => {
            document.body.innerHTML = `
            <div class="page">
                <div class="title">💖 Отличный выбор!</div>
                <button onclick="send(${index+1})">
                    Напиши мне число, время и номер свидания
                </button>
            </div>
            `;
        };

        container.appendChild(btn);
    });
};

/* ОТПРАВКА */
function send(num) {
    const text = encodeURIComponent("Я выбираю свидание №" + num + " 💖");
    window.location.href = "https://t.me/@vers_hik" + text;
}
</script>

</body>
</html>
