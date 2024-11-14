
<script>
// @ts-nocheck
    let {nombre, genero, duracion,año, precio, eliminarHandler,editarHandler} = $props();
    
</script>

<div class="p-2 bg-blue-700 w-80 h-50 rounded-md drop-shadow-md hover:scale-105  hover:bg-blue-950 hover:drop-shadow-lg transition-all duration-200 flex flex-col">
    <h2 class=" text-yellow-500 font-bold text-2xl">{nombre}</h2>
    <p class= "text-white"> {duracion}</p>
    <p class= "text-white"> {genero}</p>
    <p class= "text-white"> {año}</p>
    <div class="flex justify-end">
        <p class="text-amber-300 font-bold text-3xl">{precio}$</p>
    </div>
    <div class="flex gap-2">
        <button class="text-white font-bold flex items-center gap-2" onclick={eliminarHandler}>
            <img src="/src/images/basura.png" alt="Eliminar" class="w-6 h-6" /> 
        </button>
        <button class="text-white font-bold flex items-center gap-2" onclick={editarHandler}>
            <img src="/src/images/editar.png" alt="Editar" class="w-6 h-6" /> 
        </button>
  </div>
</div>