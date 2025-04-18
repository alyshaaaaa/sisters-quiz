# sisters-quiz
# Adjust the existing HTML for better mobile responsiveness

mobile_friendly_html = html_no_music.replace(
    "<style>",
    """<meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>"""
).replace(
    "max-width: 500px;",
    "max-width: 90vw;"
).replace(
    "font-size: 20px;",
    "font-size: 5vw;"  # scale question font size for mobile
).replace(
    "font-size: 18px;",
    "font-size: 4.5vw;"  # scale result font size for mobile
)

# Save the updated mobile-friendly HTML
mobile_html_path = "/mnt/data/sisters_quiz_mobile"
os.makedirs(mobile_html_path, exist_ok=True)
html_mobile_file = os.path.join(mobile_html_path, "index.html")

with open(html_mobile_file, "w", encoding="utf-8") as f:
    f.write(mobile_friendly_html)

# Zip the mobile version
zip_mobile_path = "/mnt/data/姜家姊妹心理測驗_10題_無音樂_手機版.zip"
with zipfile.ZipFile(zip_mobile_path, 'w') as zipf:
    for foldername, subfolders, filenames in os.walk(mobile_html_path):
        for filename in filenames:
            file_path = os.path.join(foldername, filename)
            arcname = os.path.relpath(file_path, mobile_html_path)
            zipf.write(file_path, arcname=arcname)

zip_mobile_path
