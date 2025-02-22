<script setup>
defineProps(['producto'])
defineEmits(['eliminar-producto', 'actualizar-producto'])
</script>

<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
    <p class="font-bold mb-3 text-gray-700 uppercase">
      Codigo:
      <span class="font-normal normal-case">
        {{ producto.id }}
      </span>
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
      Descripcion:
      <span class="font-normal normal-case">
        {{ producto.Descripcion }}
      </span>
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
        Stock:
        <span class="font-normal normal-case">
            {{ producto.Stock }}
        </span> 
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
        Precio:
        <span class="font-normal normal-case">
            {{ producto.Precio }}
        </span>
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
        Vencimiento:
        <span class="font-normal normal-case">
            {{ producto.Vencimiento }}
        </span>
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
        Creacion:
        <span class="font-normal normal-case">
            {{ producto.Creacion }}
        </span>
    </p>
    <p class="font-bold mb-3 text-gray-700 uppercase">
        Proveedor:
        <span class="font-normal normal-case">
            {{ producto.Proveedor }}
        </span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-10">
      <button
        type="button"
        class="block w-full py-2 px-10 bg-green-600 hover:bg-yellow-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('actualizar-producto', producto.id)"
      >
        Editar
      </button>

      <button
        type="button"
        class="block w-full py-2 px-10 bg-orange-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('eliminar-producto', producto.id)"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>
