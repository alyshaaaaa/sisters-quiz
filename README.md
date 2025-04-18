# sisters-quiz
[女女女女女心理測驗.zip](https://github.com/user-attachments/files/19812714/_10.zip)
<audio id="bg-music" loop autoplay>
  <source src="bgmusic.mp3" type="audio/mpeg">
</audio>

<button onclick="toggleMusic()">音樂開關</button>

<script>
  const music = document.getElementById("bg-music");
  let playing = true;

  function toggleMusic() {
    if (playing) {
      music.pause();
    } else {
      music.play();
    }
    playing = !playing;
  }
</script>
<img src="heart.gif" class="effect-gif" style="display: none;" id="heart-effect" />

<script>
  document.querySelectorAll(".option").forEach(option => {
    option.addEventListener("click", () => {
      const gif = document.getElementById("heart-effect");
      gif.style.display = "block";
      gif.style.position = "absolute";
      gif.style.left = event.pageX + "px";
      gif.style.top = event.pageY + "px";
      setTimeout(() => {
        gif.style.display = "none";
      }, 1000);
    });
  });
</script>
