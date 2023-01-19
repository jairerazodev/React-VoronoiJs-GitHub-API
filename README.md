# :flags: React-VoronoiJs-GitHub-API
Diagrama de Voronoi con voronoi.js y React utilizando datos desde una API externa, en este caso la API de GitHub.

Aquí te muestro cómo puedes implementar un diagrama de Voronoi con voronoi.js y React utilizando datos desde una API externa, en este caso la API de GitHub.

Primero, debes incluir la biblioteca voronoi.js en tu proyecto de React. Puedes hacerlo instalando voronoi.js a través de npm y luego importándola en tu componente de React:

  npm install voronoi
  Copy code
  import Voronoi from 'voronoi';

Luego, puedes utilizar la función `fetch()` de JavaScript para obtener los datos desde la API de GitHub. Esta función también devuelve una promesa, por lo que debes utilizar una función async/await para obtener los datos:

    async componentDidMount() {
      const response = await fetch('https://api.github.com/users');
      const data = await response.json();
      // ...
    }

Una vez que tienes los datos, puedes generar el diagrama de Voronoi utilizando la función Voronoi.compute(). Esta función toma como entrada un array de puntos y devuelve un objeto con las regiones del diagrama:

  const diagram = Voronoi.compute(data, {
    xl: 0,
    xr: 100,
    yt: 0,
    yb: 100
  });

Para dibujar el diagrama en un elemento del DOM, puedes utilizar un elemento SVG y añadir líneas y polígonos para dibujar las regiones del diagrama. En este ejemplo, utilizaremos un elemento ref para obtener una referencia al elemento SVG y luego dibujar los elementos con `d3.select()`:

  const svg = d3.select(this.refs.svg);

    svg.selectAll("path")
      .data(diagram.cells)
      .enter().append("path")
      .attr("d", cell => "M" + cell.join("L") + "Z")
      .attr("fill", "none")
      .attr("stroke", "black");

Para aplicar estilos CSS a los elementos del diagrama, puedes utilizar atributos de estilo en `d3.select()`:

  svg.selectAll("path")
    .attr("style", "fill: red; stroke: black; stroke-width: 1px;")
