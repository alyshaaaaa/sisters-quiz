# sisters-quiz
# Rebuild with full 10-question content and background music, including revised subtitle
 "<body>",
    """<body>
<audio id="bg-music" autoplay loop>
  <source src="https://youtu.be/aLuShQwNYRE?si=l9t621xmndiyFzGx" type="audio/mpeg">
</audio>
<button class="toggle-music" onclick="toggleMusic()">🔊 音樂開關</button>
html_with_questions = html_content.replace(
    "const questions = [ ... ];",
    """
    const questions = [
        { text: "1. 假日最想做什麼？", options: [
            { text: "看星盤、塔羅、靜靜發呆", type: "姜嵐嵐" },
            { text: "躺平耍廢補眠", type: "姜宜宜" },
            { text: "出門拍照、約會、逛街", type: "姜卉卉" },
            { text: "學習新技能、讀書或工作", type: "姜芮芮" },
            { text: "安排滿檔行程，全都要", type: "姜妤妤" }
        ]},
        { text: "2. 你對自己的描述最貼近哪一句？", options: [
            { text: "我有點怪怪的，但很真實", type: "姜嵐嵐" },
            { text: "我安靜但觀察力超強", type: "姜宜宜" },
            { text: "我是全場最閃亮的存在", type: "姜卉卉" },
            { text: "我是別人口中的優等生", type: "姜芮芮" },
            { text: "我控制慾有點強但我知道自己要什麼", type: "姜妤妤" }
        ]},
        { text: "3. 面對壓力時你會？", options: [
            { text: "睡一覺裝作沒事", type: "姜宜宜" },
            { text: "直接吵一架也不怕", type: "姜妤妤" },
            { text: "偷偷掉眼淚再裝沒事", type: "姜芮芮" },
            { text: "上社群發一張自拍平衡心情", type: "姜卉卉" },
            { text: "查星象說服自己一切都是命", type: "姜嵐嵐" }
        ]},
        { text: "4. 最不能接受別人說你什麼？", options: [
            { text: "沒腦", type: "姜芮芮" },
            { text: "沒氣質", type: "姜卉卉" },
            { text: "不切實際", type: "姜嵐嵐" },
            { text: "情緒太多", type: "姜妤妤" },
            { text: "太邊緣", type: "姜宜宜" }
        ]},
        { text: "5. 最喜歡的場合是？", options: [
            { text: "一個人坐在咖啡廳看書", type: "姜宜宜" },
            { text: "台上燈光打下來的那一刻", type: "姜卉卉" },
            { text: "掌握會議主導權的時候", type: "姜妤妤" },
            { text: "家裡靜靜灌溉盆栽的時候", type: "姜芮芮" },
            { text: "深夜聊天室大家互相療癒", type: "姜嵐嵐" }
        ]},
        { text: "6. 你對戀愛的態度是？", options: [
            { text: "無聊才談戀愛，愛自己比較實在", type: "姜芮芮" },
            { text: "戀愛就是要轟轟烈烈", type: "姜卉卉" },
            { text: "只談精神戀愛，肉體太麻煩", type: "姜宜宜" },
            { text: "我很容易暈船，也很容易醒", type: "姜嵐嵐" },
            { text: "戀愛可以，但我得掌控全局", type: "姜妤妤" }
        ]},
        { text: "7. 你最在意什麼？", options: [
            { text: "被忽略的感覺", type: "姜宜宜" },
            { text: "別人比我強", type: "姜妤妤" },
            { text: "沒人欣賞我", type: "姜卉卉" },
            { text: "一切都沒意義", type: "姜嵐嵐" },
            { text: "做錯事辜負期待", type: "姜芮芮" }
        ]},
        { text: "8. 別人常說你？", options: [
            { text: "太靜了", type: "姜宜宜" },
            { text: "太浮誇", type: "姜卉卉" },
            { text: "太倔強", type: "姜芮芮" },
            { text: "太感性", type: "姜嵐嵐" },
            { text: "太強勢", type: "姜妤妤" }
        ]},
        { text: "9. 你最常說的一句話？", options: [
            { text: "我覺得你這樣不行", type: "姜妤妤" },
            { text: "這個我來查一下星象", type: "姜嵐嵐" },
            { text: "拍一張再說", type: "姜卉卉" },
            { text: "好我來查一下資料", type: "姜芮芮" },
            { text: "喔，好", type: "姜宜宜" }
        ]},
        { text: "10. 你最嚮往的生活？", options: [
            { text: "獨自旅行寫日記", type: "姜宜宜" },
            { text: "在舞台上被萬人追捧", type: "姜卉卉" },
            { text: "當一個專業知識份子", type: "姜芮芮" },
            { text: "身邊有值得依靠的人和自由", type: "姜妤妤" },
            { text: "經營Podcast陪伴孤單的人", type: "姜嵐嵐" }
        ]}
    ];
    """
)

# Save corrected HTML with full questions
with open(html_file_path, "w", encoding="utf-8") as f:
    f.write(html_with_questions)

# Zip everything again
corrected_zip_path = "/mnt/data/女女女女女心理測驗.zip"
with zipfile.ZipFile(corrected_zip_path, 'w') as zipf:
    for foldername, subfolders, filenames in os.walk(project_path):
        for filename in filenames:
            file_path = os.path.join(foldername, filename)
            arcname = os.path.relpath(file_path, project_path)
            zipf.write(file_path, arcname=arcname)

corrected_zip_path
