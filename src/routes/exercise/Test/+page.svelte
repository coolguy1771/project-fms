<script>
    import P5 from 'p5-svelte'
    let exercise = window.location.pathname.split('/')[2]
  
    function done(exercise){
      console.log(exercise)
    }
  
    const sketch = (p5) => {
      let bgcolor = 'white';
      let sel = p5.createSelect();
      p5.setup = () => {
        p5.createCanvas(900, 600);
        p5.background(bgcolor);
        p5.setupCanvas();
        console.log('setup done')
      }
      p5.setupCanvas = () => {
        p5.noStroke();
        let colorPicker = p5.createColorPicker('#000000');
        colorPicker.position(10, 50);

        sel.position(150, 50);
        sel.option("Normal Paint Brush (press 'N')");
        sel.option("Splatter Brush (press 'S')");
        sel.option("Eraser (press 'E')");
        sel.option("Draw Rectangle (press 'Q')");
        sel.option("Draw Triangle (press 'T')");

        //create a slider
        let slider = p5.createSlider(1, 100, 20, 1);
        slider.position(370, 50);
        slider.style('width', '180px');

        let button = p5.createButton("Erase Canvas (press 'R')");
        button.position(650, 50);
        button.mousePressed(p5.clearBG);
        console.log('canvas setup')
      }


      
  
      p5.draw = () => {
          
        p5.noStroke();
        p5.fill('#d3d3d3');
        p5.rect(0, 0, p5.width, 100);

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
          if (sel.value() == "Normal Paint Brush (press 'N')") {

            p5.stroke(colorPicker.color());
            p5.strokeWeight(slider.value());
            p5.line(p5.pmouseX, p5.pmouseY, p5.mouseX, p5.mouseY);
          }
          if (sel.value() == "Splatter Brush (press 'S')") {

            for (i = 0; i < p5.random(1, 10); i++) {
              
              p5.noStroke();

              p5.fill(colorPicker.color());

              p5.ellipse(p5.mouseX + p5.random(-100, 100), p5.mouseY + p5.random(-100, 100), slider.value(), slider.value());
            }
          }
          if (sel.value() == "Eraser (press 'E')") {
            //eraser

            //draw a line in background color
            p5.stroke(bgcolor);
            p5.strokeWeight(slider.value());
            p5.line(p5.pmouseX, p5.pmouseY, p5.mouseX, p5.mouseY);
          }
          if (sel.value() == "Draw Rectangle (press 'Q')") {
            //draw rectangle with brush thickness at mousex and y
            p5.fill(colorPicker.color());
            p5.rect(p5.mouseX, p5.mouseY, slider.value(), slider.value());
          }
          if (sel.value() == "Draw Triangle (press 'T')") {
            
            p5.fill(colorPicker.color());
            p5.triangle(p5.mouseX, p5.mouseY, p5.mouseX + slider.value(), p5.mouseY + slider.value(), p5.mouseX - slider.value(), p5.mouseY + slider.value());
          }
        }
      }
    
      p5.clearBG=()=> { 
        p5.fill(bgcolor);
        p5.noStroke();
        p5.rect(0, 100, p5.width, p5.height - 100);
      }
      p5.keyPressed=()=> {

        if (p5.key == 'n' || p5.key == 'N') {
          
          sel.selected("Normal Paint Brush (press 'N')");
        } else if (p5.key == 's' || p5.key == 'S') {
          
          sel.selected("Splatter Brush (press 'S')");
        } else if (p5.key == 'e' || p5.key == 'E') {
          
          sel.selected("Eraser (press 'E')");
        } else if (p5.key == '+') {

          slider.value(slider.value() + 1);
        } else if (p5.key == '-') {
          
          slider.value(slider.value() - 1);
        } else if (p5.key == 'r' || p5.key == 'R') {

          p5.clearBG();
        } else if (p5.key == 'c' || p5.key == 'C') {
          
          let randomColor = "#" + p5.Math.floor(p5.Math.random() * 16777215).toString(16);
          let colorPicker = p5.createColorPicker(randomColor);
          colorPicker.position(10, 50);
        } else if (p5.key == 'q'|| p5.key == 'Q'){

          sel.selected("Draw Rectangle (press 'Q')");
        }else if (p5.key == 't'|| p5.key == 'T'){
        
          sel.selected("Draw Triangle (press 'T')");
        }

      }
    }
  </script>
  
  <div class="content">
      <P5 {sketch} />
  </div>
  
  <style>
    .content {
      border: 1px solid #ed225d;
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
  