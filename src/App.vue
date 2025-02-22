<script setup>
  import { reactive, ref, watch, onMounted } from 'vue'
  import { uid } from 'uid'
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Producto from './components/Producto.vue'

  const productos = ref([])
  const producto = reactive({
    Codigo: null,
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
    if (producto.Codigo) {
      const index = productos.value.findIndex((producto) => producto.Codigo === producto.Codigo)
      productos.value[index] = { ...producto }
    } else {
      productos.value.push({ ...producto, Codigo: uid() })
    }

    Object.assign(producto, {
      Descripcion: '',
      Stock: '',
      Precio: '',
      Vencimiento: '',
      Creacion: '',
      Proveedor: '',
      Codigo: null
    })
  }

  const eliminarProducto = (Codigo) => {
    if (confirm('¿Estás seguro de eliminar este producto de tu inventario?')) {
      productos.value = productos.value.filter((producto) => producto.Codigo !== Codigo)
      Object.assign(producto, {
        Descripcion: '',
        Stock: '',
        Precio: '',
        Vencimiento: '',
        Creacion: '',
        Proveedor: '',
        Codigo: null
    })
    }
  }

  const actualizarProducto = (Codigo) => {
    const productoEditar = producto.value.find((producto) => producto.Codigo === Codigo)
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
        :Codigo="producto.Codigo"
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
            :key="producto.Codigo"
            @eliminar-producto="eliminarProducto"
            @actualizar-producto="actualizarProducto"
          />
        </div>

        <p v-else class="mt-20 text-2xl text-center">No hay productos en el inventario</p>
      </div>
    </div>
  </div>
</template>