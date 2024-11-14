<script>
  // @ts-nocheck
  import ItemPelicula from "$lib/components/ItemPelicula.svelte";
  
  let peliculas = [
    {
      nombre: "Aladdín",
      genero: "Película infantil",
      duracion: "1h 30m",
      año: "1992",
      precio: 15.00,
    },
  ];
  
  let nombrePelicula = "";
  let generoPelicula = "";
  let duracionPelicula = "";
  let añoPelicula = "";
  let precioPelicula = "";
  
  /** @type {{ nombre: string; genero: string; duracion: string; año: string; precio: number; } | null} */
  let selectedPelicula = null;
  
  const clearInputs = () => {
    nombrePelicula = '';
    generoPelicula = '';
    duracionPelicula = '';
    añoPelicula = '';
    precioPelicula = '';
    selectedPelicula = null;
  };
  
  const agregarPelicula = (event) => {
    event.preventDefault();
    if (selectedPelicula) {
      // Buscar la película en el array y actualizarla
      peliculas = peliculas.map(pelicula =>
        pelicula === selectedPelicula
          ? {
              nombre: nombrePelicula,
              genero: generoPelicula,
              duracion: duracionPelicula,
              año: añoPelicula,
              precio: parseFloat(precioPelicula),
            }
          : pelicula
      );
      selectedPelicula = null; 
    } else {
      let nuevo = {
        nombre: nombrePelicula,
        genero: generoPelicula,
        duracion: duracionPelicula,
        año: añoPelicula,
        precio: parseFloat(precioPelicula),
      };
      peliculas = [...peliculas, nuevo];
    }
    clearInputs();
  };
  
  const eliminarPelicula = (nombre) => {
    peliculas = peliculas.filter((pelicula) => pelicula.nombre !== nombre);
  };
  
  const editarPelicula = (pelicula) => {
    selectedPelicula = pelicula;
    nombrePelicula = pelicula.nombre;
    generoPelicula = pelicula.genero;
    duracionPelicula = pelicula.duracion;
    añoPelicula = pelicula.año;
    precioPelicula = pelicula.precio.toString();
  };
</script>
  
  <div class="bg-yellow-100 h-screen px-5 flex flex-col items-center">
    <div class="flex justify-center items-center mb-5">
      <img src="/src/images/blockbuster.png" alt="Blockbuster" class="h-40 w-auto" />
    </div>
    <form
      class="bg-blue-700 mt-5 p-5 rounded-xl drop-shadow-md flex w-fit gap-5 items-center justify-evenly"
      on:submit={agregarPelicula}
    >
      <div>
        <label class="font-bold" for="nombre">NOMBRE:</label>
        <input
          type="text"
          name="nombre"
          id="nombre"
          class="border-slate-200 border-[1px] rounded-md"
          bind:value={nombrePelicula}
        />
      </div>
      <div>
        <label class="font-bold" for="genero">GÉNERO:</label>
        <input
          type="text"
          name="genero"
          id="genero"
          class="border-slate-200 border-[1px] rounded-md"
          maxlength="70"
          bind:value={generoPelicula}
        />
      </div>
      <div>
        <label class="font-bold" for="duracion">DURACIÓN:</label>
        <input
          type="text"
          name="duracion"
          id="duracion"
          class="border-grey-200 border-[1px] rounded-md"
          maxlength="70"
          bind:value={duracionPelicula}
        />
      </div>
      <div>
        <label class="font-bold" for="año">AÑO:</label>
        <input
          type="text"
          name="año"
          id="año"
          class="border-slate-200 border-[1px] rounded-md"
          bind:value={añoPelicula}
        />
      </div>
      <div>
        <label class="font-bold" for="precio">PRECIO:</label>
        <input
          type="number"
          name="precio"
          id="precio"
          min="0.1"
          class="border-slate-200 border-[1px] rounded-md"
          bind:value={precioPelicula}
        />
      </div>
      <button
        class="bg-yellow-500 text-white p-2 rounded-md font-bold hover:scale-105 hover:bg-yellow-800 transition-all duration-200"
      >
        {selectedPelicula ? 'Actualizar' : 'Guardar'}
      </button>
      <button
        type="button"
        class="bg-yellow-500 text-white p-2 rounded-md font-bold hover:scale-105 hover:bg-yellow-800 transition-all duration-200"
        on:click={clearInputs}
      >
        Limpiar
      </button>
    </form>
  
    <div
      class="mt-4 flex justify-evenly items-center flex-wrap gap-5 overflow-auto max-h-[75%]"
    >
      {#each peliculas as pelicula (pelicula.nombre)}
        <ItemPelicula
          {pelicula}
         nombre={pelicula.nombre}
         genero={pelicula.genero}
         duracion={pelicula.duracion}
         año={pelicula.año}
         precio={pelicula.precio}
          eliminarHandler={() => eliminarPelicula(pelicula.nombre)}
          editarHandler={() => editarPelicula(pelicula)}
        />
      {/each}
    </div>
  </div>
  