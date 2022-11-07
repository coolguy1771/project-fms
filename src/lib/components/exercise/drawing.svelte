<script>
  import P5 from 'p5-svelte'

  const sketch = (p5) => {
    let t = 0 // time variable

    p5.setup = () => {
      p5.createCanvas(865, 400)
      p5.noStroke()
      p5.fill('#ed225d')
    }

    p5.draw = () => {
      p5.background(10, 10) // translucent background (creates trails)

      // make a x and y grid of ellipses
      for (let x = 0; x <= p5.width; x = x + 30) {
        for (let y = 0; y <= p5.height; y = y + 30) {
          // starting point of each circle depends on mouse position
          const xAngle = p5.map(
            p5.mouseX,
            0,
            p5.width,
            -4 * p5.PI,
            4 * p5.PI,
            true
          )
          const yAngle = p5.map(
            p5.mouseY,
            0,
            p5.height,
            -4 * p5.PI,
            4 * p5.PI,
            true
          )

          // and also varies based on the particle's location
          const angle = xAngle * (x / p5.width) + yAngle * (y / p5.height)

          // each particle moves in a circle
          const myX = x + 20 * p5.cos(2 * p5.PI * t + angle)
          const myY = y + 20 * p5.sin(2 * p5.PI * t + angle)

          p5.ellipse(myX, myY, 5) // draw particle
        }
      }

      t = t + 0.005 // update time
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
    background-color: #ed225d;
    color: white;
    font-size: 1.5rem;
    font-weight: bold;
    cursor: pointer;
  }
</style>
