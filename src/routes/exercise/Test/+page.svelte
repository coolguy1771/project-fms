<script>
    import P5 from 'p5-svelte'
    let exercise = window.location.pathname.split('/')[2]
  
    function done(exercise){
      console.log(exercise)
    }
    const sketch = (p5) => {
      let bgcolor = 'white';
  
      p5.setup = () => {
        p5.createCanvas(900, 600);
        p5.background(bgcolor);
        p5.setupCanvas();
      }
      p5.setupCanvas = ()=> {
        p5.noStroke();
        p5.colorPicker = p5.createColorPicker('#000000');
        p5.colorPicker.position(10, 50);

        p5.sel = createSelect();
        p5.sel.position(150, 50);
        p5.sel.option("Normal Paint Brush (press 'N')");
        p5.sel.option("Splatter Brush (press 'S')");
        p5.sel.option("Eraser (press 'E')");
        p5.sel.option("Draw Rectangle (press 'Q')");
        p5.sel.option("Draw Triangle (press 'T')");

        //create a slider
        p5.slider = p5.createSlider(1, 100, 20, 1);
        p5.slider.position(370, 50);
        p5.slider.style('width', '180px');

        p5.button = p5.createButton("Erase Canvas (press 'R')");
        p5.button.position(650, 50);
        p5.button.mousePressed(clearBG);

      }


      
  
      p5.draw = () => {
          
        p5.noStroke();
        p5.fill('#d3d3d3');
        p5.rect(0, 0, width, 100);

        p5.fill('black');
        p5.textSize(16);
        p5.text("Brush & Eraser Thickness \n (press '+' to increase, '-' to decrease):", 370, 20);

        p5.fill('black');
        p5.textSize(16);
        p5.text("Brush Type/Eraser", 150, 30);

        p5.fill('black');
        p5.textSize(12);
        p5.text("Color of brush \n (press 'C' for a \n random color):", 10, 15);

        if (p5.mouseIsPressed && p5.mouseY > 100) {
          if (p5.sel.value() == "Normal Paint Brush (press 'N')") {

            stroke(p5.colorPicker.color());
            strokeWeight(p5.slider.value());
            line(p5.pmouseX, p5.pmouseY, p5.mouseX, p5.mouseY);
          }
          if (p5.sel.value() == "Splatter Brush (press 'S')") {

            for (i = 0; i < random(1, 10); i++) {
              
              p5.noStroke();

              p5.fill(p5.colorPicker.color());

              p5.ellipse(p5.mouseX + random(-100, 100), p5.mouseY + random(-100, 100), p5.slider.value(), p5.slider.value());
            }
          }
          if (p5.sel.value() == "Eraser (press 'E')") {
            //eraser

            //draw a line in background color
            p5.stroke(bgcolor);
            p5.strokeWeight(slider.value());
            p5.line(p5.pmouseX, p5.pmouseY, p5.mouseX, p5.mouseY);
          }
          if (p5.sel.value() == "Draw Rectangle (press 'Q')") {
            //draw rectangle with brush thickness at mousex and y
            p5.fill(p5.colorPicker.color());
            p5.rect(p5.mouseX, p5.mouseY, p5.slider.value(), p5.slider.value());
          }
          if (p5.sel.value() == "Draw Triangle (press 'T')") {
            
            p5.fill(p5.colorPicker.color());
            p5.triangle(p5.mouseX, p5.mouseY, p5.mouseX + p5.slider.value(), p5.mouseY + p5.slider.value(), p5.mouseX - p5.slider.value(), p5.mouseY + p5.slider.value());
          }
        }
      }
      p5.clearBG=()=> { 
        p5.fill(bgcolor);
        p5.noStroke();
        p5.rect(0, 100, width, height - 100);
      }
      p5.keyPressed=()=> {

        if (key == 'n' || key == 'N') {
          
          p5.sel.selected("Normal Paint Brush (press 'N')");
        } else if (key == 's' || key == 'S') {
          
          p5.sel.selected("Splatter Brush (press 'S')");
        } else if (key == 'e' || key == 'E') {
          
          p5.sel.selected("Eraser (press 'E')");
        } else if (key == '+') {

          p5.slider.value(slider.value() + 1);
        } else if (key == '-') {
          
          p5.slider.value(slider.value() - 1);
        } else if (key == 'r' || key == 'R') {

          p5.clearBG();
        } else if (key == 'c' || key == 'C') {
          
          let randomColor = "#" + p5.Math.floor(Math.random() * 16777215).toString(16);
          p5.colorPicker = p5.createColorPicker(randomColor);
          p5.colorPicker.position(10, 50);
        } else if (key == 'q'|| key == 'Q'){

          p5.sel.selected("Draw Rectangle (press 'Q')");
        }else if (key == 't'|| key == 'T'){
        
          p5.sel.selected("Draw Triangle (press 'T')");
        }

      }

  </script>
  
  <div class="content">
    <div class="p5Canvas">
      <P5 {sketch} />
    </div>
  
    
  </div>
  
  <style>
    .p5Canvas {
      border: 1px solid #ed225d;
      width: 100%;
      height: 100%;
    }
    button {
      position: absolute;
      bottom: 0;
      right: 0;
      margin: 1rem;
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 0.5rem;
      background-color: green;
      color: white;
      font-size: 1.5rem;
      font-weight: bold;
      cursor: pointer;
    }
  </style>
  