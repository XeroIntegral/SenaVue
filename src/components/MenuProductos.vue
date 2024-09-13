<template>

    <nav>
        <article>
            <div class="ubicaBotones">

                <button @click="MostrarCatergoria">
                    <img type="submit" src="../assets/categoria250x50.png" value="Muestra__Categoria">
                    <h5>Categoria</h5>
                </button>

                <button class="Proveedor_style" @click="MostrarProveedor">
                    <img type="submit" src="../assets/proveedor250x50.png" value="Muestra__Proveedor">
                    <h5>Proveedor</h5>
                </button>
                <button @click="MostrarProducto">
                    <img type="submit" src="../assets/Producto.png" value="Muestra__Producto">
                    <h5>Producto</h5>
                </button>

            </div>
        </article>
    </nav>

</template>

<script>

export default{
    methods:{
        MostrarCatergoria(){
            this.$emit('cambiarVista','categoria');
        },
        MostrarProveedor(){
            this.$emit('cambiarVista','proveedor');
        },
        MostrarProducto(){
            this.$emit('cambiarVista','producto');
        }
    }
}
</script>

<style scoped>
.ubicaBotones {
    display: flex;
     padding: auto;
}

nav article div div {
    display: flex;
    padding: 2px;
    position: relative;
    border-radius: 10%;

}

button:hover {
    background: #4F4050;
}

button:active {
    background: #4F4050;
}

nav {
    width: 240px;
    margin: 5px;
    padding: 5px;
}
</style>
