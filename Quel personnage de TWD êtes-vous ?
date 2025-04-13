<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel personnage de The Walking Dead êtes-vous ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #1b1b1b;
      color: #f2f2f2;
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #e53935;
      text-shadow: 2px 2px 5px #000;
      font-size: 36px;
      margin-bottom: 20px;
    }

    img.logo {
      max-width: 200px;
      margin-bottom: 20px;
    }

    .question {
      margin: 20px 0;
      background-color: #2c2c2c;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(229, 57, 53, 0.5);
    }

    .options button {
      background-color: #e53935;
      color: #fff;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #b71c1c;
      transform: scale(1.1);
    }

    .result {
      background-color: #2c2c2c;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(229, 57, 53, 0.5);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #ff8a80;
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/15/j84n.jpeg" alt="Logo The Walking Dead">
  <h1>Quel personnage de The Walking Dead êtes-vous ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <p class="score">Votre résultat est basé sur vos choix !</p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>

  <script>
    const questions = [
      { question: "Que faites-vous face à un danger immédiat ?", options: ["Agir vite", "Observer avant d'agir", "Protéger les autres", "Fuir pour survivre"], result: [0, 1, 2, 3] },
      { question: "Quel est votre rôle idéal dans un groupe ?", options: ["Leader", "Conseiller", "Protecteur", "Éclaireur"], result: [4, 5, 6, 7] },
      { question: "Votre plus grand défaut ?", options: ["Trop impulsif", "Trop distant", "Trop attaché", "Trop méfiant"], result: [8, 9, 0, 1] },
      { question: "Comment gérez-vous une trahison ?", options: ["Colère", "Silence", "Dialogue", "Éloignement"], result: [2, 3, 4, 5] },
      { question: "Quel type d’arme préférez-vous ?", options: ["Katana", "Arbalète", "Revolver", "Couteau"], result: [6, 7, 8, 9] },
      { question: "Quelle est votre priorité ?", options: ["La justice", "La famille", "La survie", "La loyauté"], result: [0, 1, 2, 3] },
      { question: "Quel est votre plus grand atout ?", options: ["Discrétion", "Détermination", "Force mentale", "Compassion"], result: [4, 5, 6, 7] },
      { question: "Quel est votre plus grand cauchemar ?", options: ["Être seul", "Perdre le contrôle", "Échouer", "Devenir un monstre"], result: [8, 9, 0, 1] },
      { question: "Comment vos proches vous décriraient ?", options: ["Fidèle", "Protecteur", "Indépendant", "Ténébreux"], result: [2, 3, 4, 5] },
      { question: "Quel est votre objectif ?", options: ["Reconstruire", "Survivre en paix", "Protéger le groupe", "Punir ceux qui détruisent"], result: [6, 7, 8, 9] }
    ];

    const characters = [
      { name: "Rick Grimes", description: "Ancien shérif, leader naturel prêt à tout pour protéger son groupe." },
      { name: "Daryl Dixon", description: "Chasseur taciturne et fidèle, un survivant né au cœur d'or caché." },
      { name: "Michonne", description: "Silencieuse et redoutable, elle manie le katana avec une sagesse froide." },
      { name: "Carol Peletier", description: "Fragile au départ, elle est devenue une stratège aussi redoutable qu’humaine." },
      { name: "Glenn Rhee", description: "Rapide, malin et loyal, un cœur courageux dans un monde cruel." },
      { name: "Negan", description: "Charismatique et brutal, il est capable de cruauté comme de rédemption." },
      { name: "Maggie Greene", description: "Déterminée et juste, elle ne recule devant rien pour défendre les siens." },
      { name: "Carl Grimes", description: "Jeune survivant mûri trop vite, il incarne l'espoir d'un avenir meilleur." },
      { name: "Rosita Espinosa", description: "Combattante farouche, débrouillarde et loyale jusqu’au bout." },
      { name: "Eugene Porter", description: "Intelligent mais réservé, souvent sous-estimé, il se révèle essentiel au groupe." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];

      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
