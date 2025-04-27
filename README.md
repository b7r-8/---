import os
from zipfile import ZipFile

# Root directory for final website files
root_dir = '/mnt/data/baher_alakwad_site_final'

# Define directory structure
dirs = [
    root_dir,
    os.path.join(root_dir, 'assets'),
    os.path.join(root_dir, 'assets', 'css'),
    os.path.join(root_dir, 'assets', 'js'),
    os.path.join(root_dir, 'assets', 'img'),
]

# Create directories
for d in dirs:
    os.makedirs(d, exist_ok=True)

# Create HTML files with basic structure
html_templates = {
    'index.html': '<!DOCTYPE html>\n<html lang="ar" data-theme="light">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>بحر الأكواد - الصفحة الرئيسية</title>\n  <link rel="icon" href="assets/img/favicon.png">\n  <link rel="stylesheet" href="assets/css/styles.min.css">\n</head>\n<body>\n  <header>\n    <h1>مرحبا بك في بحر الأكواد</h1>\n    <button id="theme-toggle">تبديل الوضع</button>\n  </header>\n  <main>\n    <div id="timer">10s</div>\n    <!-- محتوى الأكواد هنا -->\n  </main>\n  <script src="assets/js/scripts.min.js"></script>\n</body>\n</html>',
    'codes.html': '<!DOCTYPE html>\n<html lang="ar" data-theme="light">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>بحر الأكواد - الأكواد</title>\n  <link rel="stylesheet" href="assets/css/styles.min.css">\n</head>\n<body>\n  <header><h1>صفحة الأكواد</h1></header>\n  <main>\n    <!-- قائمة الأكواد -->\n  </main>\n  <script src="assets/js/scripts.min.js"></script>\n</body>\n</html>',
    'advertise.html': '<!DOCTYPE html>\n<html lang="ar" data-theme="light">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>بحر الأكواد - أعلن معنا</title>\n  <link rel="stylesheet" href="assets/css/styles.min.css">\n</head>\n<body>\n  <header><h1>أعلن معنا</h1></header>\n  <main>\n    <!-- معلومات الإعلانات -->\n  </main>\n  <script src="assets/js/scripts.min.js"></script>\n</body>\n</html>',
    'contact.html': '<!DOCTYPE html>\n<html lang="ar" data-theme="light">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>بحر الأكواد - اتصل بنا</title>\n  <link rel="stylesheet" href="assets/css/styles.min.css">\n</head>\n<body>\n  <header><h1>اتصل بنا</h1></header>\n  <main>\n    <!-- نموذج الاتصال -->\n  </main>\n  <script src="assets/js/scripts.min.js"></script>\n</body>\n</html>',
    'about.html': '<!DOCTYPE html>\n<html lang="ar" data-theme="light">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>بحر الأكواد - عن الموقع</title>\n  <link rel="stylesheet" href="assets/css/styles.min.css">\n</head>\n<body>\n  <header><h1>عن بحر الأكواد</h1></header>\n  <main>\n    <!-- نبذة عن الموقع -->\n  </main>\n  <script src="assets/js/scripts.min.js"></script>\n</body>\n</html>',
}

# Write HTML files
for filename, content in html_templates.items():
    with open(os.path.join(root_dir, filename), 'w', encoding='utf-8') as f:
        f.write(content)

# Placeholder CSS, JS, image, and PDF files
css_path = os.path.join(root_dir, 'assets', 'css', 'styles.min.css')
js_path = os.path.join(root_dir, 'assets', 'js', 'scripts.min.js')
img_path = os.path.join(root_dir, 'assets', 'img', 'favicon.png')
pdf_path = os.path.join(root_dir, 'intro.pdf')

with open(css_path, 'w', encoding='utf-8') as f:
    f.write('/* Minified CSS placeholder */')
with open(js_path, 'w', encoding='utf-8') as f:
    f.write('// Minified JS placeholder')
with open(img_path, 'wb') as f:
    f.write(b'\x89PNG\r\n\x1a\n')  # minimal PNG header
with open(pdf_path, 'wb') as f:
    f.write(b'%PDF-1.4\n%Placeholder PDF\n')

# Create final zip archive
zip_filename = '/mnt/data/baher-alakwad-site-final.zip'
with ZipFile(zip_filename, 'w') as zipf:
    for root, dirs, files in os.walk(root_dir):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, root_dir)
            zipf.write(file_path, arcname)

zip_filename
