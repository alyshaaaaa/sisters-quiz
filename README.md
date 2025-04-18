# sisters-quiz
[女女女女女心理測驗.zip](https://github.com/user-attachments/files/19812714/_10.zip)
# Add background music to the existing 10-question version of the quiz

music_file_url = "https://cdn.pixabay.com/download/audio/2023/03/28/audio_7c763a1ec4.mp3?filename=calm-lofi-hip-hop-141051.mp3"
music_tag = f"""
<audio id="bg-music" autoplay loop>
  <source src="{music_file_url}" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<button onclick="toggleMusic()">🔊 音樂開關</button>
<script>
    const music = document.getElementById("bg-music");
    let isPlaying = true;
    function toggleMusic() {{
        if (isPlaying) {{
            music.pause();
        }} else {{
            music.play();
        }}
        isPlaying = !isPlaying;
    }}
</script>
"""

# Load the current HTML and inject music elements
html_file_path = "/mnt/data/sisters_quiz_10_questions/index.html"
with open(html_file_path, "r", encoding="utf-8") as file:
    html_lines = file.readlines()

# Inject the music player after <body> tag
updated_html_lines = []
for line in html_lines:
    updated_html_lines.append(line)
    if "<body>" in line:
        updated_html_lines.append(music_tag)

# Write updated HTML
with open(html_file_path, "w", encoding="utf-8") as file:
    file.writelines(updated_html_lines)

# Zip updated version
zip_path_music = "/mnt/data/姜家姊妹心理測驗_10題_含背景音樂版.zip"
with zipfile.ZipFile(zip_path_music, 'w') as zipf:
    for foldername, subfolders, filenames in os.walk("/mnt/data/sisters_quiz_10_questions"):
        for filename in filenames:
            file_path = os.path.join(foldername, filename)
            arcname = os.path.relpath(file_path, "/mnt/data/sisters_quiz_10_questions")
            zipf.write(file_path, arcname=arcname)

zip_path_music
