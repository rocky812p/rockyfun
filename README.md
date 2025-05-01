# rockyfun
movie-website/
├── index.html
├── login.html
├── admin.html
├── style.css
├── script.js
├── firebase-config.js
├── images/
│   └── logo.png (आपकी वेबसाइट का लोगो)
└── README.md
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
// Replace with your Firebase config
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT.firebaseio.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "XXXX",
  appId: "XXXX"
};
firebase.initializeApp(firebaseConfig);
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Movie Stream</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>🎬 Movie World</h1>
    <input type="text" id="search" placeholder="Search movie..." />
  </header>

  <section id="movie-list"></section>

  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-database.js"></script>
  <script src="firebase-config.js"></script>
  <script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Admin Login</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="login-box">
    <h2>Admin Login</h2>
    <input type="email" id="email" placeholder="Email" />
    <input type="password" id="password" placeholder="Password" />
    <button onclick="login()">Login</button>
  </div>

  <script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-auth.js"></script>
  <script src="firebase-config.js"></script>
  <script>
    function login() {
      const email = document.getElementById("email").value;
      const pass = document.getElementById("password").value;
      firebase.auth().signInWithEmailAndPassword(email, pass)
        .then(() => window.location.href = "admin.html")
        .catch(e => alert("Login Failed"));
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Upload Movie</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h2>Upload New Movie</h2>
  <input id="title" placeholder="Title" />
  <input id="desc" placeholder="Description" />
  <input id="thumb" placeholder="Thumbnail URL" />
  <input id="video" placeholder="Video Stream URL" />
  <input id="quality" placeholder="Quality" />
  <input id="language" placeholder="Language" />
  <input id="category" placeholder="Category" />
  <button onclick="uploadMovie()">Upload</button>

  <script src="firebase-config.js"></script>
  <script>
    function uploadMovie() {
      const data = {
        title: title.value,
        desc: desc.value,
        thumb: thumb.value,
        url: video.value,
        quality: quality.value,
        language: language.value,
        category: category.value,
      };
      firebase.database().ref("movies").push(data)
        .then(() => alert("Movie uploaded!"))
        .catch(err => alert("Error: " + err));
    }
  </script>
</body>
</html>
body {
  font-family: sans-serif;
  background: #111;
  color: white;
  margin: 0;
  padding: 0;
}
header {
  padding: 20px;
  background: #222;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
#search {
  padding: 10px;
  width: 200px;
  border: none;
  border-radius: 5px;
}
#movie-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding: 20px;
}
.movie-card {
  background: #1c1c1c;
  border-radius: 10px;
  overflow: hidden;
  transition: 0.3s;
}
.movie-card:hover {
  transform: scale(1.05);
}
.movie-card img {
  width: 100%;
}
.movie-card h3 {
  padding: 10px;
}
.login-box {
  max-width: 300px;
  margin: 50px auto;
  background: #222;
  padding: 20px;
  border-radius: 10px;
}
.login-box input, .login-box button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
}
firebase.database().ref("movies").on("value", snapshot => {
  const movies = snapshot.val();
  const list = document.getElementById("movie-list");
  list.innerHTML = "";

  for (let id in movies) {
    const m = movies[id];
    const card = `
      <div class="movie-card">
        <img src="${m.thumb}" />
        <h3>${m.title}</h3>
        <p>${m.language} | ${m.quality}</p>
        <video controls width="100%" src="${m.url}" controlsList="nodownload"></video>
      </div>
    `;
    list.innerHTML += card;
  }
});
git init
git remote add origin https://github.com/username/movie-website.git
git add .
git commit -m "Initial Commit"
git push -u origin main
