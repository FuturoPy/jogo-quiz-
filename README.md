<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Escolar 🎓</title>
<style>
  body {
    font-family: "Comic Sans MS", Arial, sans-serif;
    background: linear-gradient(180deg, #eaf6ff, #ffffff);
    text-align: center;
    margin: 0;
    padding: 40px;
  }

  .quiz-container {
    background-color: #ffffff;
    border-radius: 20px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
    max-width: 700px;
    margin: auto;
    padding: 30px;
    position: relative;
    overflow: hidden;
  }

  h1 {
    color: #0078d7;
    margin-bottom: 10px;
  }

  .area-jogo {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 25px;
  }

  .professor {
    width: 200px;
    height: 260px;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    transition: 0.3s ease;
  }

  .conteudo {
    text-align: left;
    flex: 1;
  }

  .pergunta {
    font-size: 22px;
    font-weight: bold;
    margin: 20px 0;
  }

  button {
    background-color: #0078d7;
    color: white;
    border: none;
    border-radius: 12px;
    padding: 12px 20px;
    margin: 6px 0;
    font-size: 17px;
    cursor: pointer;
    transition: 0.3s;
    width: 100%;
  }

  button:hover {
    background-color: #005fa3;
    transform: scale(1.03);
  }

  .feedback {
    font-size: 22px;
    font-weight: bold;
    margin-top: 20px;
    text-align: center;
  }

  .correct { color: green; }
  .wrong { color: red; }

  /* Confete */
  .confetti {
    position: fixed;
    width: 10px;
    height: 10px;
    background-color: red;
    animation: fall 2s linear forwards;
    z-index: 999;
  }
  @keyframes fall {
    0% {transform: translateY(0) rotate(0);}
    100% {transform: translateY(800px) rotate(720deg);}
  }
</style>
</head>
<body>

<div class="quiz-container">
  <h1>Quiz Escolar 🎓</h1>

  <div class="area-jogo">
    <div class="professor" id="professor"
         style="background-image: url('https://cdn-icons-png.flaticon.com/512/3063/3063825.png');">
    </div>

    <div class="conteudo">
      <div id="question" class="pergunta"></div>
      <div id="answers"></div>
      <div id="feedback" class="feedback"></div>
    </div>
  </div>
</div>

<script>
const perguntas = [
  {
    pergunta: "📚 Português: Qual dessas palavras está escrita corretamente?",
    opcoes: ["Excessão", "Exceção", "Exceçâo"],
    certa: 1
  },
  {
    pergunta: "🧮 Matemática: Quanto é 8 + 7?",
    opcoes: ["15", "16", "14"],
    certa: 0
  },
  {
    pergunta: "🌎 Geografia: Qual é o maior oceano do mundo?",
    opcoes: ["Atlântico", "Pacífico", "Índico"],
    certa: 1
  },
  {
    pergunta: "🔬 Ciências: Qual planeta é conhecido como 'planeta vermelho'?",
    opcoes: ["Marte", "Júpiter", "Vênus"],
    certa: 0
  },
  {
    pergunta: "🏛️ História: Quem foi o primeiro presidente do Brasil?",
    opcoes: ["Dom Pedro II", "Deodoro da Fonseca", "Getúlio Vargas"],
    certa: 1
  }
];

let indice = 0;
const professor = document.getElementById("professor");
const feedback = document.getElementById("feedback");

function mostrarPergunta() {
  const q = perguntas[indice];
  document.getElementById("question").textContent = q.pergunta;
  const respostasDiv = document.getElementById("answers");
  respostasDiv.innerHTML = "";
  feedback.textContent = "";

  // Professor apontando para o lado (posição padrão)
  professor.style.backgroundImage = "url('https://cdn-icons-png.flaticon.com/512/3063/3063825.png')";

  q.opcoes.forEach((opcao, i) => {
    const btn = document.createElement("button");
    btn.textContent = opcao;
    btn.onclick = () => checkAnswer(i === q.certa);
    respostasDiv.appendChild(btn);
  });
}

function checkAnswer(certa) {
  if (certa) {
    feedback.textContent = "🎉 Muito bem!";
    feedback.className = "feedback correct";
    professor.style.backgroundImage = "url('https://cdn-icons-png.flaticon.com/512/3063/3063807.png')"; // professor feliz
    soltarConfete();
    setTimeout(() => {
      indice++;
      if (indice < perguntas.length) mostrarPergunta();
      else {
        document.querySelector(".quiz-container").innerHTML =
          "<h1>🎊 Parabéns! Você terminou o quiz! 👏</h1><p>O professor está muito orgulhoso de você! 🧑‍🏫</p>";
      }
    }, 1800);
  } else {
    feedback.textContent = "😅 Tente novamente!";
    feedback.className = "feedback wrong";
    professor.style.backgroundImage = "url('https://cdn-icons-png.flaticon.com/512/3063/3063836.png')"; // professor pensativo
  }
}

function soltarConfete() {
  for (let i = 0; i < 50; i++) {
    const confete = document.createElement("div");
    confete.classList.add("confetti");
    confete.style.left = Math.random() * window.innerWidth + "px";
    confete.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
    confete.style.animationDuration = (1.5 + Math.random()) + "s";
    document.body.appendChild(confete);
    setTimeout(() => confete.remove(), 2000);
  }
}

mostrarPergunta();
</script>

</body>
</html>
