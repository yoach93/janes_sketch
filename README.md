<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>p5.js Sketch</title>
    <style>
      body {
        margin: 0;
        padding: 0;
        overflow: hidden;
      }
      canvas {
        display: block;
      }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
  </head>
  <body>
    <script>
      let words = [];
      let wordList = ["ךמצע", "תא", "אונשלו", "רקובב", "ררועתהל", "םדרהל", "םלעהל", "חוכשלו", "חורבל"];
      let sentenceLines = [
        ",חוכשלו חורבל",
        "םדרהל םלעהל",
        "רקובב ררועתהל",
        "ךמצע תא אונשלו",
        "ההההההההההההההההא"
      ];
      let numRepeats = 300;
      let startRadius = 500;
      let customFont;
      let yOffset = 0;
      let scrollSpeed = 10;

      function preload() {
        customFont = loadFont('https://raw.githubusercontent.com/yoach93/janes_sketch/main/myfont.otf'); // Update with your URL
      }

      function setup() {
        createCanvas(windowWidth, windowHeight);
        textAlign(CENTER, CENTER);
        textSize(6);
        angleMode(DEGREES);
        textFont(customFont);

        for (let j = 0; j < numRepeats; j++) {
          wordList.forEach(word => {
            let angle = random(360);
            let distance = random(startRadius);
            words.push({ char: word, angle: angle, initialDistance: distance, distance: distance });
          });
        }
      }

      function draw() {
        background('#F4F3F2');
        translate(width / 2, height / 2);

        words.forEach(word => {
          word.distance = word.initialDistance + yOffset;
          let x = cos(word.angle) * word.distance;
          let y = sin(word.angle) * word.distance;

          fill(0);
          text(word.char, x, y);
        });

        textSize(30);
        fill(0);

        let lineHeight = 40;
        for (let i = 0; i < sentenceLines.length; i++) {
          text(sentenceLines[i], 0, -80 + i * lineHeight);
        }
      }

      function windowResized() {
        resizeCanvas(windowWidth, windowHeight);
      }

      function mouseWheel(event) {
        yOffset += event.delta * scrollSpeed;
        yOffset = constrain(yOffset, 0, height * 10);
      }
    </script>
  </body>
</html>
