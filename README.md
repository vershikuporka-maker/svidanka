<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Patrick+Hand&display=swap" rel="stylesheet">

<title>Для тебя ❤️</title>

<style>
body {
    margin: 0;
    background: #fffdf7;
    font-family: 'Patrick Hand', cursive;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
}

/* ЗАГОЛОВОК */
.title {
    font-size: 26px;
    text-align: center;
    padding: 20px;
    border: 3px dashed #333;
    border-radius: 20px;
    position: relative;
}

/* КОТ НАД ТЕКСТОМ */
.cat-on-title {
    position: absolute;
    top: -30px;
    right: 10px;
    font-size: 30px;
}

/* КНОПКИ */
button {
    margin: 10px;
    padding: 15px 20px;
    font-size: 18px;
    border-radius: 15px;
    border: 2px solid #333;
    background: white;
    cursor: pointer;
}

/* ДА */
#yes {
    background: #caffbf;
}

/* НЕТ */
#no {
    background: #ffadad;
}

/* СПИСОК */
.list {
    width: 90%;
    max-width: 500px;
    margin-top: 20px;
}

.list button {
    width: 100%;
    text-align: left;
    margin: 8px 0;
}

/* КОТИКИ */
.cat {
    position: absolute;
    font-size: 20px;
    animation: run 10s linear infinite;
}

@keyframes run {
    0% { left: -50px; }
    100% { left: 110%; }
}
</style>
</head>

<body>

<div class="title">
    Пойдешь со мной на свидание? 💖
    <div class="cat-on-title">🐱</div>
</div>

<button id="yes">ДА</button>
<button id="no">НЕТ</button>

<!-- БЕГАЮЩИЕ КОТИКИ -->
<div class="cat" style="top:20%">🐈</div>
<div class="cat" style="top:50%; animation-delay:2s">🐈‍⬛</div>
<div class="cat" style="top:70%; animation-delay:4s">🐈</div>

<script>
const noBtn = document.getElementById("no");

/* НЕТ УМЕНЬШАЕТСЯ */
noBtn.addEventListener("click", () => {
    noBtn.style.transform = "scale(0.2)";
});

/* ДА → СТРАНИЦА */
document.getElementById("yes").onclick = () => {

    document.body.innerHTML = `
    <div class="title">Выбирай свидание 🐱</div>
    <div class="list" id="dates"></div>

    <div class="cat" style="top:20%">🐈</div>
    <div class="cat" style="top:60%; animation-delay:3s">🐈‍⬛</div>
    `;

    const ideas = [
        "1. Чтение друг другу книг вслух, с эмоциями, как актеры.",
        "2. Пешеходная прогулка до рассвета.",
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
            <div class="title">💖 Отличный выбор!</div>
            <button onclick="send(${index+1})">
                Напиши мне число, время и номер свидания
            </button>
            `;
        };

        container.appendChild(btn);
    });
};

/* ОТПРАВКА */
function send(num) {
    const text = encodeURIComponent("Я выбираю свидание №" + num + " 💖");
    window.location.href = "https://t.me/ВАШ_НИК?text=" + text;
}
</script>

</body>
</html>
