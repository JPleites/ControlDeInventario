<script setup>
import { reactive } from 'vue'
import Alerta from './Alerta.vue'

const props = defineProps({
  Descripcion: {
    type: String,
    default: '',
  },
  Stock: {
    type: String,
    default: '',
  },
  Precio:{
    type: String,
    default: '',
  },
  Vencimiento: {
    type: String,
    default: '',
  },
  Creacion:{
    type: String,
    default: '',
  },
  Proveedor:{
    type: String,
    default: '',
  },
  Codigo: {
    type: String,
    default: null,
  }
})

const emits = defineEmits([
  'guardar-producto',
  'update:Descripcion',
  'update:Stock',
  'update:Precio',
  'update:Vencimiento',
  'update:Creacion',
  'update:Proveedor'
])

const alerta = reactive({
  mensaje: '',
  tipo: ''
})

const handleSubmit = (e) => {
  e.preventDefault()
  if (Object.values(props).includes('')) {
    alerta.mensaje = 'Todos los campos son obligatorios'
    alerta.tipo = 'error'
    return
  }

  emits('guardar-producto')

  alerta.mensaje = `Producto ${props.Codigo ? 'editado' : 'creado'} correctamente`
  alerta.tipo = 'exito'

  if (alerta.mensaje) {
    setTimeout(() => {
      alerta.mensaje = ''
      alerta.tipo = ''
    }, 3000)
  }
}
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Añade productos al <span class="text-indigo-600 font-bold">Inventario</span>
    </p>

    <Alerta v-if="alerta.mensaje" :mensaje="alerta.mensaje" :tipo="alerta.tipo" />

    <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit="handleSubmit">
      <div class="mb-5">
        <label for="Descripcion" class="block text-gray-700 font-bold">Descripcion</label>
        <input
          type="text"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Descripcion"
          name="Descripcion"
          :value="Descripcion"
          @input="$emit('update:Descripcion', $event.target.value)"
          placeholder="Nombre o descripcion del producto"
        />
      <div>
        <label for="Stock" class="block text-gray-700 font-bold">Stock</label>
        <input
          type="text"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Stock"
          name="Stock"
          :value="Stock"
          @input="$emit('update:Stock', $event.target.value)"
          placeholder="Cantidad en stock del producto"
        />
      </div>
      <div>
        <label for="Precio" class="block text-gray-700 font-bold">Precio</label>
        <input
          type="text"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Precio"
          name="Precio"
          :value="Precio"
          @input="$emit('update:Precio', $event.target.value)"
          placeholder="Precio del producto"
        />
      </div>
      <div>
        <label for="Vencimiento" class="block text-gray-700 font-bold">Vencimiento</label>
        <input
          type="date"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Vencimiento"
          name="Vencimiento"
          :value="Vencimiento"
          @input="$emit('update:Vencimiento', $event.target.value)"
        />
      </div>
      <div>
        <label for="Creacion" class="block text-gray-700 font-bold">Creacion</label>
        <input
          type="date"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Creacion"
          name="Creacion"
          :value="Creacion"
          @input="$emit('update:Creacion', $event.target.value)"
        />
      </div>
      <div>
        <label for="Proveedor" class="block text-gray-700 font-bold">Proveedor</label>
        <input
          type="text"
          class="border-2 w-full mt-2 p-2 rounded-md placeholder-gray-400 outline-gray-400"
          id="Proveedor"
          name="Proveedor"
          :value="Proveedor"
          @input="$emit('update:Proveedor', $event.target.value)"
          placeholder="Nombre del proveedor"
        />
      </div>

      </div>
      <button
        type="submit"
        class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-md w-full mt-5 transition-all uppercase"
      >
        {{ Codigo ? 'Editar Producto' : 'Agregar Producto' }}
      </button>
    </form>
  </div>
</template>