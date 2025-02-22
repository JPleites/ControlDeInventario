<script setup>
  import { reactive, ref, watch, onMounted } from 'vue'
  import { uid } from 'uid'
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Producto from './components/Producto.vue'

  const productos = ref([])
  const producto = reactive({
    id: null,
    Descripcion: '',
    Stock: '',
    Precio: '',
    Vencimiento: '',
    Creacion: '',
    Proveedor: '',
  })

  watch(
    productos,
    (productosWatch) => {
      localStorage.setItem('productos', JSON.stringify(productosWatch))
    },
    { deep: true }
  )
  onMounted(() => {
    const productosLocalStorage = JSON.parse(localStorage.getItem('productos'))
    if (productosLocalStorage) productos.value = productosLocalStorage
  })

  const guardarProducto = () => {
    if (producto.id) {
      const index = productos.value.findIndex((producto) => producto.id === producto.id)
      productos.value[index] = { ...producto }
    } else {
      productos.value.push({ ...producto, id: uid() })
    }

    Object.assign(producto, {
      Descripcion: '',
      Stock: '',
      Precio: '',
      Vencimiento: '',
      Creacion: '',
      Proveedor: '',
      id: null
    })
  }

  const eliminarProducto = (id) => {
    if (confirm('¿Estás seguro de eliminar este producto de tu inventario?')) {
      productos.value = productos.value.filter((producto) => producto.id !== id)
      Object.assign(producto, {
        Descripcion: '',
        Stock: '',
        Precio: '',
        Vencimiento: '',
        Creacion: '',
        Proveedor: '',
        id: null
    })
    }
  }

  const actualizarProducto = (id) => {
    const productoEditar = productos.value.find((producto) => producto.id === id)
    Object.assign(producto, productoEditar)
  }
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex gap-5 p-4">
      <Formulario
        v-model:Descripcion="producto.Descripcion"
        v-model:Stock="producto.Stock"
        v-model:Precio="producto.Precio"
        v-model:Vencimiento="producto.Vencimiento"
        v-model:Creacion="producto.Creacion"
        v-model:Proveedor="producto.Proveedor"
        :id="producto.id"
        @guardar-producto="guardarProducto"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-auto">
        <h2 class="font-black text-3xl text-center">Inventario</h2>
        <p class="text-lg mt-5 text-center mb-10">
          Hay <span class="text-indigo-600 font-bold">{{ productos.length }}</span> productos en tu inventario
        </p>

        <div v-if="productos.length > 0">
          <Producto
            v-for="producto in productos"
            :producto="producto"
            :key="producto.id"
            @eliminar-producto="eliminarProducto"
            @actualizar-producto="actualizarProducto"
          />
        </div>

        <p v-else class="mt-20 text-2xl text-center">No hay productos en el inventario</p>
      </div>
    </div>
  </div>
</template>