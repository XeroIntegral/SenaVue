<template>
  <div class="contenedor">
    
      <div class="components-menu">
        <MenuProductos @cambiarVista="cambiarComponente" />
      </div>

      <div class="components-tablas">
        <div v-if="componenteActual === 'categoria'" class="CategoriaVisible">
          <TablaCategoria />
        </div>

        <div v-if="componenteActual === 'proveedor'" class="ProveedorVisible">
          <TablaProveedor />
        </div>

        <div v-if="componenteActual === 'producto'" class="ProductosVisible">
          <TablaProductos />
        </div>

      </div>
   
  </div>  

</template>

<script>
import MenuProductos from "@/components/MenuProductos.vue";
import TablaCategoria from "@/components/TablaCategoria.vue";
import TablaProveedor from "@/components/TablaProveedores.vue";
import TablaProductos from "@/components/TablaProductos.vue";

export default { 

  components: {
    MenuProductos,
    TablaProductos,
    TablaCategoria,
    TablaProveedor
  },
  data(){
    return {
      componenteActual:'producto' //metodo por defecto
    };
  },
  methods:{
    cambiarComponente(vista){
      this.componenteActual=vista;
    }
  }
}

</script>

<style scoped>
.contenedor {

  display: flex;
  flex-direction: row; /* Asegura que los elementos estén uno al lado del otro */
  justify-content: flex-start; /* Da espacio entre el menú y la tabla */
  align-items: flex-start; /* Alinea ambos elementos en la parte superior */
  padding-top: 130px; /* Ajuste para evitar que el menú se superponga al contenido */
}

.components-menu {
  width: 15%; /* Menú ocupa menos espacio, ajusta el tamaño aquí */
  padding: 1px; /* Puedes reducir el padding para disminuir el espacio */
}

.components-tablas {
  width: 80%; /* Tabla ocupa más espacio */
  padding: 1px; /* Puedes reducir o quitar el padding aquí */
  margin-left: 1px; /* Controla el espacio entre el menú y la tabla */
}
</style>