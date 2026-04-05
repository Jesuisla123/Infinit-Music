from pathlib import Path
import zipfile
import webbrowser

# Dossier de l'application
base = Path("riffa_app")
base.mkdir(exist_ok=True)

# Contenu des fichiers
index = """<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Riffa</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <header>
      <img src="logo.svg" class="logo" alt="Riffa logo">
      <h1>Riffa</h1>
      <p class="tagline">Reconnais une musique. Découvre son histoire. Crée ton remix.</p>
    </header>

    <main>
      <button id="recordBtn">🎙️ Reconnaître une musique</button>

      <section id="result" class="card hidden">
        <h2>Résultat</h2>
        <p><strong>Titre :</strong> <span id="title"></span></p>
        <p><strong>Compositeur :</strong> <span id="composer"></span></p>
        <p><strong>Date de composition :</strong> <span id="compositionDate"></span></p>
        <p><strong>Date de publication :</strong> <span id="releaseDate"></span></p>
      </section>

      <section id="remix" class="card hidden">
        <h2>Remix personnalisé</h2>
        <textarea id="mood" placeholder="Exemple : remix plus électro, plus rapide, ambiance nuit..."></textarea>
        <button id="remixBtn">Créer une idée de remix</button>
        <div id="remixResult"></div>
      </section>
    </main>
  </div>

  <script src="app.js"></script>
</body>
</html>
"""

css = """body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #0f172a, #1e293b);
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.container { width: 90%; max-width: 700px; }
header { text-align: center; margin-bottom: 30px; }
.logo { width: 90px; margin-bottom: 10px; }
h1 { font-size: 3rem; margin: 0; }
.tagline { color: #cbd5e1; }
button { width: 100%; padding: 15px; border: none; border-radius: 14px; background: #8b5cf6; color: white; font-size: 1rem; cursor: pointer; margin-top: 10px; }
button:hover { background: #7c3aed; }
.card { background: rgba(255,255,255,0.08); padding: 20px; border-radius: 18px; margin-top: 20px; backdrop-filter: blur(10px); }
.hidden { display: none; }
textarea { width: 100%; min-height: 100px; border-radius: 12px; border: none; padding: 12px; margin-top: 10px; resize: vertical; }
"""

js = """const recordBtn = document.getElementById('recordBtn');
const result = document.getElementById('result');
const remix = document.getElementById('remix');

recordBtn.addEventListener('click', async () => {
  const music = { title: "Clair de Lune", composer: "Claude Debussy", compositionDate: "1905", releaseDate: "1905" };
  document.getElementById('title').textContent = music.title;
  document.getElementById('composer').textContent = music.composer;
  document.getElementById('compositionDate').textContent = music.compositionDate;
  document.getElementById('releaseDate').textContent = music.releaseDate;
  result.classList.remove('hidden'); remix.classList.remove('hidden');
});

document.getElementById('remixBtn').addEventListener('click', () => {
  const mood = document.getElementById('mood').value;
  document.getElementById('remixResult').innerHTML = `
    <p>🎧 Proposition :</p>
    <ul>
      <li>Accélérer le tempo de 15%</li>
      <li>Ajouter une basse électronique profonde</li>
      <li>Créer une ambiance : ${mood || "cinématique et moderne"}</li>
      <li>Utiliser une reverb légère sur le piano</li>
    </ul>
  `;
});
"""

svg = """<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 200 200">
  <defs><linearGradient id="g" x1="0%" y1="0%" x2="100%" y2="100%">
  <stop offset="0%" stop-color="#8b5cf6"/><stop offset="100%" stop-color="#22d3ee"/>
  </linearGradient></defs>
  <circle cx="100" cy="100" r="80" fill="url(#g)"/>
  <path d="M120 50 v60 a20 20 0 1 1 -10 -17 V70 l40 -10 v50 a20 20 0 1 1 -10 -17 V50z" fill="white"/>
</svg>
"""

# Écriture des fichiers
(base/"index.html").write_text(index)
(base/"style.css").write_text(css)
(base/"app.js").write_text(js)
(base/"logo.svg").write_text(svg)

# Ouvrir la page web dans Safari
webbrowser.open(str(base/"index.html"))

print("Projet créé et ouvert dans Safari !")
