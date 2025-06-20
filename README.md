<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>Moteur de recherche IA avec ChatGPT</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background: #f7f7f7;
    }
    h1 {
      color: #4f46e5;
      text-align: center;
    }
    #question {
      width: 80%;
      padding: 12px;
      font-size: 18px;
      margin: 10px auto;
      display: block;
      border: 2px solid #4f46e5;
      border-radius: 8px;
    }
    #btn {
      display: block;
      margin: 0 auto 20px;
      background-color: #4f46e5;
      color: white;
      font-size: 18px;
      padding: 10px 30px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    #response {
      max-width: 800px;
      margin: 20px auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 8px #aaa;
      white-space: pre-wrap;
    }
  </style>
</head>
<body>
  <h1>Moteur de recherche IA avec ChatGPT</h1>
  <input type="text" id="question" placeholder="Pose ta question ici..." />
  <button id="btn">Rechercher</button>
  <div id="response">La réponse apparaîtra ici.</div>

  <script>
    const btn = document.getElementById("btn");
    const responseDiv = document.getElementById("response");

    btn.addEventListener("click", async () => {
      const question = document.getElementById("question").value.trim();
      if (!question) {
        alert("Veuillez poser une question.");
        return;
      }
      responseDiv.textContent = "Chargement...";
      try {
        const res = await fetch("https://api.openai.com/v1/chat/completions", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": "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"
          },
          body: JSON.stringify({
            model: "gpt-3.5-turbo",
            messages: [{ role: "user", content: question }],
            temperature: 0.7
          })
        });
        if (!res.ok) throw new Error("Erreur API : " + res.status);
        const data = await res.json();
        const answer = data.choices[0].message.content;
        responseDiv.textContent = answer;
      } catch (error) {
        responseDiv.textContent = "Erreur : " + error.message;
      }
    });
  </script>
</body>
</html>
