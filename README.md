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
    justify-content: center;
    align-items: center;
    flex-direction: column;
    overflow: hidden;

    /* 🔥 ТВОЙ ФОН */
    background: url("bg.jpg") no-repeat center/cover;
}

/* затемнение для читаемости */
body::before {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    background: rgba(255,255,255,0.6);
    z-index: 0;
}

.page {
    position: relative;
    z-index: 2;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 90%;
    max-width: 420px;
    text-align: center;
}

.title {
    font-size: 26px;
    padding: 20px;
    border: 3px solid black;
    border-radius: 20px;
    background: white;
    box-shadow: 4px 4px 0 black;
    margin-bottom: 20px;
    position: relative;
}

.cat-top {
    position: absolute;
    top: -25px;
    right: 10px;
    font-size: 28px;
}

/* КНОПКИ */
button {
    width: 100%;
    margin: 8px 0;
    padding: 15px;
    font-size: 18px;
    border-radius: 20px;
    border: 3px solid black;
    background: white;
    box-shadow: 3px 3px 0 black;
    cursor: pointer;
}

button:active {
    transform: translate(2px,2px);
}

#yes { background: #baffc9; }
#no { background: #ffb3ba; }

/* 🐱 БЕГАЮЩИЕ КОТИКИ */
.cat {
    position: absolute;
    font-size: 26px;
    animation: run linear infinite;
}

@keyframes run {
    0% { transform: translateX(-100px); }
    100% { transform: translateX(120vw); }
}

/* 💖 СЕРДЕЧКИ */
.heart {
    position: absolute;
    animation: float 1s ease-out forwards;
}

@keyframes float {
    0% { opacity:1; transform: translateY(0); }
    100% { opacity:0; transform: translateY(-80px); }
}
</style>
</head>

<body>

<div id="app"></div>

<!-- 🎵 МУЗЫКА -->
<audio id="music" src="music.mp3" loop></audio>
<audio id="purr" src="purr.mp3"></audio>

<script>
const app = document.getElementById("app");

/* 🎵 запуск музыки при первом касании */
document.addEventListener("click", () => {
    document.getElementById("music").play();
}, { once: true });

/* ---------- СТРАНИЦА 1 ---------- */
function page1() {
    app.innerHTML = `
    <div class="page">
        <div class="title">
            Пойдешь со мной на свидание? 💖
            <div class="cat-top">🐱</div>
        </div>

        <button id="yes">ДА</button>
        <button id="no">НЕТ</button>
    </div>

    ${catsHTML()}
    `;

    document.getElementById("no").onclick = () => {
        const btn = document.getElementById("no");
        btn.style.transform = "scale(0.2)";
    };

    document.getElementById("yes").onclick = page2;

    initCats();
}

/* ---------- СТРАНИЦА 2 ---------- */
function page2() {
    app.innerHTML = `
    <div class="page">
        <div class="title">Выбирай свидание 💫</div>
        <div id="list"></div>
    </div>

    ${catsHTML()}
    `;

    const ideas = [
        "1. Чтение друг другу книг вслух, с эмоциями, как актеры.",
        "2. Пешеходная прогулка до рассвета.",
        "3. Поиск созвездий.",
        "4. Совместный рисунок.",
        "5. Съемка как кино.",
        "6. Интервью.",
        "7. Истории про прохожих.",
        "8. Музей / театр."
    ];

    const list = document.getElementById("list");

    ideas.forEach((text, i) => {
        const btn = document.createElement("button");
        btn.innerText = text;
        btn.onclick = () => page3(i+1);
        list.appendChild(btn);
    });

    initCats();
}

/* ---------- СТРАНИЦА 3 ---------- */
function page3(num) {
    app.innerHTML = `
    <div class="page">
        <div class="title">💖 Отличный выбор!</div>
        <button onclick="send(${num})">
            Напиши мне число, время и номер свидания
        </button>
    </div>

    ${catsHTML()}
    `;

    initCats();
}

/* 🐱 КОТИКИ HTML */
function catsHTML() {
    return `
    <div class="cat" style="top:20%; animation-duration:8s">🐈</div>
    <div class="cat" style="top:50%; animation-duration:12s">🐈‍⬛</div>
    <div class="cat" style="top:80%; animation-duration:10s">🐈</div>
    `;
}

/* 🐱 РЕАКЦИЯ КОТОВ + МУРЧАНИЕ */
function initCats() {
    document.querySelectorAll(".cat").forEach(cat => {
        cat.onclick = () => {
            cat.innerText = "😻";
            document.getElementById("purr").play();

            setTimeout(() => cat.innerText = "🐱", 500);
        };
    });
}

/* 💖 СЕРДЕЧКИ */
document.addEventListener("click", (e) => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerText = "💖";
    heart.style.left = e.clientX + "px";
    heart.style.top = e.clientY + "px";
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 1000);
});

/* 📩 ОТПРАВКА */
function send(num) {
    const text = encodeURIComponent("Я выбираю свидание №" + num + " 💖");
    window.location.href = "https://t.me/ВАШ_НИК?text=" + text;
}

page1();
</script>

</body>
</html>
