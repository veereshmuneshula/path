<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OBS Camera Source</title>

<style>
  html, body {
    margin: 0;
    padding: 0;
    background: black;
    width: 100%;
    height: 100%;
    overflow: hidden;
    font-family: Arial, sans-serif;
  }

  #ui {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background: black;
  }

  button {
    padding: 18px 40px;
    font-size: 22px;
    font-weight: bold;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    background: #00c853;
    color: black;
  }

  video {
    display: none;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    transform: scaleX(-1); /* mirror */
  }
</style>
</head>

<body>

<div id="ui">
  <button id="connectBtn">🔌 CONNECT</button>
</div>

<video id="camera" autoplay muted playsinline></video>

<script>
  const connectBtn = document.getElementById("connectBtn");
  const video = document.getElementById("camera");
  const ui = document.getElementById("ui");

  connectBtn.onclick = async () => {
    try {
      const stream = await navigator.mediaDevices.getUserMedia({
        video: {
          width: { ideal: 1280 },
          height: { ideal: 720 },
          frameRate: { ideal: 30 }
        },
        audio: false
      });

      video.srcObject = stream;
      ui.style.display = "none";
      video.style.display = "block";

      console.log("Camera connected for OBS source");

    } catch (err) {
      alert("Camera permission denied or unavailable");
      console.error(err);
    }
  };
</script>

</body>
</html>
