<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap" rel="stylesheet">

<title>Для тебя ❤️</title>

<style>
body {
    margin: 0;
    min-height: 100vh;
    font-family: 'Comic Neue', cursive;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;

    background: url("bg.jpg") no-repeat center/cover;
}

/* затемнение */
body::before {
    content: "";
    position: fixed;
    width: 100%;
    height: 100%;
    background: rgba(255,255,255,0.6);
    z-index: 0;
}

/* контейнер */
.page {
    position: relative;
    z-index: 2;
    width: 90%;
    max-width: 420px;
    margin: 40px auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

/* заголовок */
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

/* кнопки */
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

/* список */
#list {
    width: 100%;
    padding-bottom: 40px;
}

/* коты */
.cat {
    position: fixed;
    font-size: 26px;
    animation: run linear infinite;
    z-index: 1;
}

@keyframes run {
    0% { transform: translateX(-100px); }
    100% { transform: translateX(120vw); }
}

/* сердечки */
.heart {
    position: fixed;
    animation: float 1s ease-out forwards;
    z-index: 3;
}

@keyframes float {
    0% { opacity:1; transform: translateY(0); }
    100% { opacity:0; transform: translateY(-80px); }
}
</style>
</head>

<body>

<div id="app"></div>

<audio id="music" src="music.mp3" loop></audio>
<audio id="purr" src="purr.mp3"></audio>

<script>
const app = document.getElementById("app");

/* запуск музыки */
document.addEventListener("click", () => {
    document.getElementById("music").play();
}, { once: true });

/* страница 1 */
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
        document.getElementById("no").style.transform = "scale(0.2)";
    };

    document.getElementById("yes").onclick = page2;

    initCats();
}

/* страница 2 */
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
        "2. Пешеходная прогулка до рассвета, чтобы встретить солнце вдвоем.",
        "3. Поиск созвездий и выдумывание собственных легенд о них.",
        "4. Совместный рисунок на старой простыне или большом ватмане.",
        "5. Съемка друг друга на камеру, как будто это кино.",
        "6. Спонтанное интервью друг с другом — будто вы знаменитости.",
        "7. Сидеть в людном месте и придумывать истории случайных прохожих.",
        "8. Хочу окультуриваться (музей, театры и т.д)."
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

/* страница 3 */
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

/* коты */
function catsHTML() {
    return `
    <div class="cat" style="top:20%; animation-duration:8s">🐈</div>
    <div class="cat" style="top:50%; animation-duration:12s">🐈‍⬛</div>
    <div class="cat" style="top:80%; animation-duration:10s">🐈</div>
    `;
}

function initCats() {
    document.querySelectorAll(".cat").forEach(cat => {
        cat.onclick = () => {
            cat.innerText = "😻";
            document.getElementById("purr").play();
            setTimeout(() => cat.innerText = "🐱", 500);
        };
    });
}

/* сердечки */
document.addEventListener("click", (e) => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerText = "💖";
    heart.style.left = e.clientX + "px";
    heart.style.top = e.clientY + "px";
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 1000);
});

/* отправка */
function send(num) {
    const text = encodeURIComponent("Я выбираю свидание №" + num + " 💖");
    window.location.href = "https://t.me/ВАШ_НИК?text=" + text;
}

page1();
</script>

</body>
</html>
