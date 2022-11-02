<script>
    import P5 from 'p5-svelte'
    let exercise = window.location.pathname.split('/')[2]
  
    function done(exercise){
      console.log(exercise)
    }
    const sketch = (p5) => {
      let c = 'black'
  
      p5.setup = () => {
        p5.createCanvas(p5.displayWidth, p5.displayHeight);
        p5.background(205)
      }
  
      p5.draw = () => {
        if (p5.mouseIsPressed) {
          p5.stroke(c)
          p5.line(p5.mouseX, p5.mouseY, p5.pmouseX, p5.pmouseY)
        }
  
        p5.noStroke()
        //draw the first button
        p5.fill('red')
        p5.rect(0, 0, 40, 40)
  
        //draw the second button
        p5.fill('blue')
        p5.rect(40, 0, 40, 40)
      }
  
      //this will run whenever the mouse is pressed
      p5.mousePressed = () => {
        if (p5.mouseX > 0 && p5.mouseX < 40 && p5.mouseY > 0 && p5.mouseY < 40) {
          //set the variables to random values
          c = 'red'
        }
        if (p5.mouseX > 40 && p5.mouseX < 80 && p5.mouseY > 0 && p5.mouseY < 40) {
          //set the variables to random values
          c = 'blue'
        }
      }
    }
  </script>
  
  <div class="content">
    <div class="p5Canvas">
      <P5 {sketch} />
    </div>
  
    <button>I'm done</button>
  </div>
  
  <style>
    .p5Canvas {
      border: 1px solid #ed225d;
      width: 60%;
      height: 60%;
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