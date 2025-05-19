
<html lang="ar">
<head>
<meta charset="UTF-8" />
<title>لعبة ألغاز - 100 سؤال</title>
<style>
  body {
    background: #111;
    color: #fff;
    font-family: sans-serif;
    text-align: center;
    padding: 30px;
    direction: rtl;
  }
  h1 {
    font-size: 28px;
    margin-bottom: 10px;
  }
  #question {
    font-size: 22px;
    margin: 20px auto;
    max-width: 600px;
  }
  .option {
    background: #222;
    margin: 8px auto;
    padding: 10px;
    border-radius: 8px;
    max-width: 400px;
    cursor: pointer;
    transition: background 0.3s;
  }
  .option:hover {
    background: #1e90ff;
    color: white;
  }
  #message {
    margin-top: 15px;
    font-size: 18px;
  }
  #next-btn {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 18px;
    background: green;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    display: none;
  }
</style>
</head>
<body>

<h1>لعبة الألغاز - سؤال <span id="level-num">1</span> من 100</h1>
<div id="question">جارٍ التحميل...</div>
<div id="options"></div>
<div id="message"></div>
<button id="next-btn">التالي</button>

<script>
  const questions = [
    {
      question: "ما هو عكس كلمة (سريع)؟",
      options: ["قوي", "بطيء", "حار", "بارد"],
      answer: "بطيء"
    },
    {
      question: "أي كوكب يُعرف بالكوكب الأحمر؟",
      options: ["زحل", "المريخ", "عطارد", "نبتون"],
      answer: "المريخ"
    },
    {
      question: "كم عدد أرجل العنكبوت؟",
      options: ["6", "8", "10", "4"],
      answer: "8"
    },
    {
      question: "من هو مؤسس شركة مايكروسوفت؟",
      options: ["ستيف جوبز", "مارك زوكربيرغ", "بيل غيتس", "إيلون ماسك"],
      answer: "بيل غيتس"
    },
    {
      question: "ما هو حاصل ضرب 12 × 12؟",
      options: ["124", "132", "144", "156"],
      answer: "144"
    }
  ];

  // توليد أسئلة حسابية صعبة تلقائيًا
  for (let i = 6; i <= 100; i++) {
    const num = i + 10;
    const result = num * num;
    questions.push({
      question: `ما هو ناتج ${num} × ${num}؟`,
      options: [
        String(result),
        String(result - 10),
        String(result + 20),
        String(result - 1)
      ],
      answer: String(result)
    });
  }

  let current = 0;
  const questionEl = document.getElementById("question");
  const optionsEl = document.getElementById("options");
  const messageEl = document.getElementById("message");
  const nextBtn = document.getElementById("next-btn");
  const levelNumEl = document.getElementById("level-num");

  function loadQuestion() {
    const q = questions[current];
    levelNumEl.textContent = current + 1;
    questionEl.textContent = q.question;
    optionsEl.innerHTML = "";
    messageEl.textContent = "";
    nextBtn.style.display = "none";

    q.options.sort(() => Math.random() - 0.5); // خلط الخيارات

    q.options.forEach((opt) => {
      const div = document.createElement("div");
      div.className = "option";
      div.textContent = opt;
      div.onclick = () => selectOption(div, opt);
      optionsEl.appendChild(div);
    });
  }

  function selectOption(div, selected) {
    const correct = questions[current].answer;
    if (selected === correct) {
      messageEl.style.color = "lime";
      messageEl.textContent = "إجابة صحيحة! ✅";
      nextBtn.style.display = "inline-block";
      disableOptions();
    } else {
      messageEl.style.color = "red";
      messageEl.textContent = "إجابة خاطئة، حاول مرة أخرى.";
      div.style.background = "#a00";
      div.style.color = "#fff";
      div.style.pointerEvents = "none";
    }
  }

  function disableOptions() {
    document.querySelectorAll(".option").forEach((opt) => {
      opt.style.pointerEvents = "none";
    });
  }

  nextBtn.onclick = () => {
    current++;
    if (current >= questions.length) {
      questionEl.textContent = "🎉 مبروك! أنهيت جميع الألغاز.";
      optionsEl.innerHTML = "";
      nextBtn.style.display = "none";
      messageEl.textContent = "";
    } else {
      loadQuestion();
    }
  };

  loadQuestion();
</script>

</body>
</html>\
