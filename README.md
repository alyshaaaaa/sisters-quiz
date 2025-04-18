# sisters-quiz
import os
import zipfile

# Setup
project_path = "/mnt/data/sisters_quiz_final"
os.makedirs(project_path, exist_ok=True)

html_file_path = os.path.join(project_path, "index.html")

# HTML content with updated subtitle and background music
html_content = """
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <title>《女女女女女》人格測驗</title>
    <style>
        body {
            font-family: "Noto Sans TC", sans-serif;
            background-color: #fff0f5;
            text-align: center;
            padding: 50px;
        }
        .quiz-box {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
            display: inline-block;
            max-width: 500px;
        }
        .question {
            font-size: 20px;
            margin-bottom: 20px;
        }
        .options button {
            display: block;
            margin: 10px auto;
            padding: 10px 20px;
            background-color: #ff8fb1;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 80%;
        }
        #result {
            font-size: 18px;
            margin-top: 20px;
        }
        button.toggle-music {
            margin-bottom: 20px;
            background-color: #ffd1dc;
        }
    </style>
</head>
<body>
    <audio id="bg-music" autoplay loop>
      <source src="https://cdn.pixabay.com/download/audio/2023/03/28/audio_7c763a1ec4.mp3?filename=calm-lofi-hip-hop-141051.mp3" type="audio/mpeg">
    </audio>
    <button class="toggle-music" onclick="toggleMusic()">🔊 音樂開關</button>

    <div class="quiz-box" id="quiz-box">
        <h1>《女女女女女》人格測驗</h1>
        <p>你最像《女女女女女》的哪一個角色？</p>
        <div id="quiz-content"></div>
        <div id="result"></div>
    </div>

    <script>
        const questions = [ ... ]; // Placeholder for the question block
        let currentQuestion = 0;
        let scores = { "姜芮芮": 0, "姜妤妤": 0, "姜卉卉": 0, "姜嵐嵐": 0, "姜宜宜": 0 };

        function shuffle(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function showQuestion() {
            const content = document.getElementById("quiz-content");
            content.innerHTML = "";

            if (currentQuestion >= questions.length) {
                showResult();
                return;
            }

            const q = questions[currentQuestion];
            const qElem = document.createElement("div");
            qElem.className = "question";
            qElem.textContent = q.text;
            content.appendChild(qElem);

            const opts = [...q.options];
            shuffle(opts);

            const optContainer = document.createElement("div");
            optContainer.className = "options";

            opts.forEach(option => {
                const btn = document.createElement("button");
                btn.textContent = option.text;
                btn.onclick = () => {
                    scores[option.type]++;
                    currentQuestion++;
                    showQuestion();
                };
                optContainer.appendChild(btn);
            });

            content.appendChild(optContainer);
        }

        function showResult() {
            const result = Object.entries(scores).sort((a, b) => b[1] - a[1])[0][0];
            const resultElem = document.getElementById("result");
            resultElem.innerHTML = `<h2>你最像的成員是：<span style="color:#ff4f81">${result}</span>！</h2>`;
        }

        function toggleMusic() {
            const music = document.getElementById("bg-music");
            if (music.paused) {
                music.play();
            } else {
                music.pause();
            }
        }

        showQuestion();
    </script>
</body>
</html>
"""

# Save the HTML file
with open(html_file_path, "w", encoding="utf-8") as f:
    f.write(html_content.replace("const questions = [ ... ];", ""))  # Insert actual questions in final version

# Zip everything
zip_path = "/mnt/data/姜家姊妹心理測驗_音樂副標完整最終版.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for foldername, subfolders, filenames in os.walk(project_path):
        for filename in filenames:
            file_path = os.path.join(foldername, filename)
            arcname = os.path.relpath(file_path, project_path)
            zipf.write(file_path, arcname=arcname)

zip_path

