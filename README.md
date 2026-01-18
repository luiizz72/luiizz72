<div align="center">
  <!-- Imagem de boas-vindas -->
  <img src="img/tchau.png" width="200"/>

  <br><br>

  <!-- Ferramentas -->
  <h2>🛠️ Ferramentas e Tecnologias</h2>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" width="40"/>

  <br><br>

  <!-- Estudando -->
  <h2>📚 Estou aprendendo</h2>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" width="40"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="40"/>

  <br><br>

  <!-- Redes sociais -->
  <a href="https://www.linkedin.com/in/luiz-fernando-2a01b22a8/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>

  <a href="https://mail.google.com/mail/?view=cm&to=luiz991675232@gmail.com" target="_blank">
    <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>

  <a href="https://discord.gg/ballerini-789888698673922078" target="_blank">
    <img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white"/>
  </a>

  <a href="https://www.instagram.com/luiizz_alves7/" target="_blank">
    <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/>
  </a>
</div>

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Pac-Man Simples</title>
<style>
  body {
    background: black;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  canvas {
    background: black;
    border: 3px solid yellow;
  }
</style>
</head>
<body>

<canvas id="game" width="400" height="400"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

const tileSize = 20;
const rows = 20;
const cols = 20;

let pacman = { x: 1, y: 1, dx: 0, dy: 0 };

let map = [
  "####################",
  "#........#.........#",
  "#.####.###.#.####...#",
  "#.................#",
  "#.####.#.#####.#..#",
  "#......#...#.....#",
  "######.###.#.###.##",
  "#................#",
  "#.####.#####.####.#",
  "#........#.......#",
  "#.######.#.######.#",
  "#.................#",
  "#.####.###.#.####..#",
  "#......#...#.....#",
  "######.#.#####.#.##",
  "#................#",
  "#.####.#####.####.#",
  "#........#.......#",
  "#................#",
  "####################"
];

function drawMap() {
  for (let y = 0; y < rows; y++) {
    for (let x = 0; x < cols; x++) {
      if (map[y][x] === "#") {
        ctx.fillStyle = "blue";
        ctx.fillRect(x * tileSize, y * tileSize, tileSize, tileSize);
      } else {
        ctx.fillStyle = "black";
        ctx.fillRect(x * tileSize, y * tileSize, tileSize, tileSize);

        if (map[y][x] === ".") {
          ctx.fillStyle = "white";
          ctx.beginPath();
          ctx.arc(
            x * tileSize + tileSize / 2,
            y * tileSize + tileSize / 2,
            3,
            0,
            Math.PI * 2
          );
          ctx.fill();
        }
      }
    }
  }
}

function drawPacman() {
  ctx.fillStyle = "yellow";
  ctx.beginPath();
  ctx.arc(
    pacman.x * tileSize + tileSize / 2,
    pacman.y * tileSize + tileSize / 2,
    tileSize / 2 - 2,
    0.25 * Math.PI,
    1.75 * Math.PI
  );
  ctx.lineTo(
    pacman.x * tileSize + tileSize / 2,
    pacman.y * tileSize + tileSize / 2
  );
  ctx.fill();
}

function movePacman() {
  let nextX = pacman.x + pacman.dx;
  let nextY = pacman.y + pacman.dy;

  if (map[nextY][nextX] !== "#") {
    pacman.x = nextX;
    pacman.y = nextY;

    if (map[nextY][nextX] === ".") {
      map[nextY] =
        map[nextY].substring(0, nextX) +
        " " +
        map[nextY].substring(nextX + 1);
    }
  }
}

document.addEventListener("keydown", e => {
  if (e.key === "ArrowUp") { pacman.dx = 0; pacman.dy = -1; }
  if (e.key === "ArrowDown") { pacman.dx = 0; pacman.dy = 1; }
  if (e.key === "ArrowLeft") { pacman.dx = -1; pacman.dy = 0; }
  if (e.key === "ArrowRight") { pacman.dx = 1; pacman.dy = 0; }
});

function gameLoop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drawMap();
  movePacman();
  drawPacman();
}

setInterval(gameLoop, 150);
</script>

</body>
</html>
