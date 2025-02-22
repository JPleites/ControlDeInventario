<script setup>
defineProps(['producto'])
defineEmits(['eliminar-producto', 'actualizar-producto'])
</script>

<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Descripcion:
      <span class="font-normal normal-case">
        {{ producto.Descripcion }}
      </span>
    </p>
    <p class="mx-5 my10 bg-white shadow-md px-5 py-10 rounded-xl">
        Stock:
        <span class="font-normal normal-case">
            {{ producto.Stock }}
        </span> 
    </p>
    <p class="mx-5 my10 bg-white shadow-md px-5 py-10 rounded-xl">
        Precio:
        <span class="font-normal normal-case">
            {{ producto.Precio }}
        </span>
    </p>
    <p class="mx-5 my10 bg-white shadow-md px-5 py-10 rounded-xl">
        Vencimiento:
        <span class="font-normal normal-case">
            {{ producto.Vencimiento }}
        </span>
    </p>
    <p class="mx-5 my10 bg-white shadow-md px-5 py-10 rounded-xl">
        Creacion:
        <span class="font-normal normal-case">
            {{ producto.Creacion }}
        </span>
    </p>
    <p class="mx-5 my10 bg-white shadow-md px-5 py-10 rounded-xl">
        Proveedor:
        <span class="font-normal normal-case">
            {{ producto.Proveedor }}
        </span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-10">
      <button
        type="button"
        class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('actualizar-producto', producto.Codigo)"
      >
        Editar
      </button>

      <button
        type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('eliminar-producto', producto.Codigo)"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>
