# JS-Simulator
The code source of the JavaScript simulator used in the CoVprehension.org website, with test files. It is mainly based on the [Particles.js](https://vincentgarreau.com/particles.js/) library.

# Structure

```bash
├──index_all_questions.html
├── part_css
│   └── particules.css
├── part_js
│   ├── app.js
│   ├── particles.js
│   └── scripts.js
├── vendor
│   ├── many libraries
├── README.md
└── LICENCE
```

The main file to modify to define new simulations is the `part_js / particles.js`:
  * `part_js/particles.js`: based on the `particles.js` library for the particle rendering, it adds the model dynamics. It defines some Netlogo primitives (fd, rt, one-of, n-of ...).
  * `part_js/scripts.js`: it contains mainly function to deal with play / pause of the simulations
  * `part_js/app.js`: it describes the link between an HTML element of the page and the call to the creation of a given simulation. Some parameters of the simulation can directly be modified here.

The `vendor` libraries should not be modified.


# How to add a new simulation to an HTML page

In the HTML page, the addition of a simulation is limited to adding such `<div>` block:

```
<div id="id-of-the-simulation"></div>
```

In addition, the `app.js`should be modifie in order to create a simulation in this block:

```
particlesJS('particles-js-Q2A', false,
  {
    "simulation": {
      "scenario": "Simulation 2a"
     }
  }
);
```

The previous block only specify the simulation scenario, but other parameters can be specify. The following block modify the initial value of some simulation parameters (`transmission_distance`, `distanciation_distance` and `speed`) and some particle parameters (their `size`).
```
particlesJS('particles-js-Q2B', false,
  {
    "simulation": {
      "transmission_distance": 16,
      "distanciation_distance": 30,
      "speed":5,
      "scenario": "Simulation 2b"
    },
    "particles": {
      size: {
        value: 9
      }
    }
  }
);
```

# Create a new simulation

To create a new simulation, a good starting point could be the file `particles_empty.js`, that keeps the structure of `particles.js` without all the code of the model.

Just as in a Netlogo model, you to code 2 main procedures: 
 * `setup`: `	pJS.fn.netlogo.setup = function() {`
 * `go`: `	pJS.fn.particlesUpdate = function(){` 

Finally, for additional procedures, I tried to follow the following namespaces:
 * `pJS.fn.netlogo.NAME`: for a global procedure
 * `pJS.fn.particle.prototype.NAME`: for a procedure to be applied on a particle agent.
 
