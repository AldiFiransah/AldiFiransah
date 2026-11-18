<img width="1509" height="1042" alt="Sosok Babi Bermata Merah dalam Kabut" src="https://github.com/user-attachments/assets/83e08a86-7a32-4367-bc1f-391e3c2a1e7e" />

### On My Learning Path
<p align="left">
  <img src="https://skillicons.dev/icons?i=figma,js,java,html,arch,linux" />
</p>

### Find me on
<p align="left">
  <a href="https://www.youtube.com/@Orang_hitam1" target="_blank">
    <img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" />
  </a>
  <a href="https://www.tiktok.com/@hamster_c1huy" target="_blank">
    <img src="https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white" />
  </a>
  <a href="https://discord.com" target="_blank">
    <img src="https://img.shields.io/badge/Discord-itz__alking-5865F2?style=for-the-badge&logo=discord&logoColor=white" />
  </a>
</p>


https://github.com/user-attachments/assets/7facdcad-10e3-4326-9570-ae360dfe683b

<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Radar Chart</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #160c24;
    }
    svg {
      background-color: #231438;
      border-radius: 12px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
    }
  </style>
</head>
<body>

<svg id="radar" width="400" height="400" viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <!-- Gradasi biru menyala di tengah seperti pada gambar -->
    <radialGradient id="glowFill" cx="50%" cy="50%" r="55%">
      <stop offset="0%" stop-color="#4ef2d2" />
      <stop offset="45%" stop-color="#2d8cff" />
      <stop offset="100%" stop-color="#2554ff" />
    </radialGradient>
  </defs>

  <g id="grid"></g>
  <polygon id="data-shape" fill="url(#glowFill)" opacity="0.95" />
  <g id="dots"></g>
</svg>

<script>
  // Atur nilai 6 sumbu (skala 0 - 100) searah jarum jam mulai dari atas:
  // [Atas, Kanan Atas, Kanan Bawah, Bawah, Kiri Bawah, Kiri Atas]
  const values = [70, 43, 30, 68, 50, 70];

  // Warna 6 titik di lingkaran luar
  const dotColors = ["#1e88e5", "#4dd0e1", "#ce93d8", "#ff9800", "#e91e63", "#ff5722"];

  const cx = 200, cy = 200, maxR = 140;
  const gridGroup = document.getElementById("grid");
  const dotsGroup = document.getElementById("dots");
  const polygon = document.getElementById("data-shape");

  // 1. Gambar 3 lingkaran jaring (grid)
  [0.35, 0.7, 1].forEach(scale => {
    const circle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
    circle.setAttribute("cx", cx);
    circle.setAttribute("cy", cy);
    circle.setAttribute("r", maxR * scale);
    circle.setAttribute("fill", "none");
    circle.setAttribute("stroke", "rgba(255, 255, 255, 0.12)");
    circle.setAttribute("stroke-width", "1");
    gridGroup.appendChild(circle);
  });

  // 2. Gambar 6 garis sumbu, titik warna, dan bentuk area data
  let points = [];
  values.forEach((val, i) => {
    const angle = (Math.PI / 180) * (-90 + i * 60);
    const cos = Math.cos(angle);
    const sin = Math.sin(angle);

    // Garis sumbu memanjang sedikit melewati lingkaran luar
    const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
    line.setAttribute("x1", cx);
    line.setAttribute("y1", cy);
    line.setAttribute("x2", cx + (maxR + 25) * cos);
    line.setAttribute("y2", cy + (maxR + 25) * sin);
    line.setAttribute("stroke", "rgba(255, 255, 255, 0.12)");
    line.setAttribute("stroke-width", "1");
    gridGroup.appendChild(line);

    // Titik warna di lingkaran luar
    const dot = document.createElementNS("http://www.w3.org/2000/svg", "circle");
    dot.setAttribute("cx", cx + maxR * cos);
    dot.setAttribute("cy", cy + maxR * sin);
    dot.setAttribute("r", "6");
    dot.setAttribute("fill", dotColors[i]);
    dotsGroup.appendChild(dot);

    // Koordinat sudut poligon berdasarkan nilai
    const r = (val / 100) * maxR;
    points.push(`${cx + r * cos},${cy + r * sin}`);
  });

  polygon.setAttribute("points", points.join(" "));
</script>

</body>
</html>

