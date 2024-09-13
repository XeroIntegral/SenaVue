<template>
    <div>
        <div class="titulo_tabla">
            <h3>CATEGORIAS</h3>
        </div>
    </div>

    <div>
        <form class="form-container" @submit.prevent="guardarCategoria">

            <div class="form-group">
                <label for="idcategoria">Id Categoria:</label>
                <input type="number" id="idcategoria" name="idcategoria" v-model="idcategoria" required />
            </div>

            <div class="form-group">
                <label for="nombre">Nombre Categoria:</label>
                <input type="text" id="nombre" name="nombre" v-model="nombre" required />
            </div>

            <div class="form-actions">
                <button type="submit" id="guardarCategoria" name="guardarCategoria"
                    class="btn-submit">Registrar</button>
                <button type="button" class="btn-crud" name="eliminar" id="eliminar" @click="eliminar">Eliminar</button>
                <button type="button" class="btn-crud" name="consultar" id="consultar"
                    @click="consultar">Consultar</button>
                <button type="button" class="btn-crud" name="actualizar" id="actualizar"
                    @click="actualizar">Actualizar</button>
            </div>
        </form>
    </div>

    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th> Id </th>
                    <th> Categoria </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="categoria in categorias" :key="categoria.idCategoria">
                    <td>{{ categoria.idCategoria }}</td>
                    <td>{{ categoria.nombre }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert2'

export default {
    data() {
        return {
            categorias: [],
            idcategoria: "",
            nombre: "",
            contadorerrores: 0,
            maxErrores: 5,
        };
    },
    methods: {
        guardarCategoria() {

            if (this.nombre.trim() === "") {
                swal.fire({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'El valor de categoria no puede estar vacío!',
                });
                return;
            }
            axios
                .post("http://localhost:8080/api/categoria", {
                    idcategoria: this.idcategoria,
                    nombre: this.nombre,
                })
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Categoria resgitrada',
                        text: 'La categoria ' + response.data.nombre + ' ha sido registrada correctamente!',
                    });
                    this.idcategoria = "";
                    this.nombre = "";
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al registrar la categoria!',
                    });
                    console.error("errror al registrar la categoria", error)
                });
        },
        consultar() {
            axios
                .get("http://localhost:8080/api/categoria/" + this.idcategoria)
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Id valido',
                        text: 'Categoria ' + response.data.idCategoria + 'encontrado correctamente!',
                    });
                    this.nombre = response.data.nombre;
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al Listar el Id de la categoria!',
                    });
                    console.error("errror al Consultar el Id de la categoria", error)
                });
        },
        actualizar() {
            axios
                .put("http://localhost:8080/api/categoria/actualizar/" + this.idcategoria, {
                    idCategoria: this.idcategoria,
                    nombre: this.nombre,
                })
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Actualizacion Realizada',
                        text: 'categoria ' + response.data.nombre + ' actualizada correctamente!',
                    });
                    this.idcategoria = "";
                    this.nombre = "";
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error actualizar la categoria!',
                    });
                    console.error("errror al actualizar la categoria", error)
                });
        },
        eliminar() {
            axios
                .delete("http://localhost:8080/api/categoria/" + this.idcategoria)
                .then(() => {
                    swal.fire({
                        icon: 'success',
                        title: 'categoria eliminada',
                        text: 'Categoria Eliminada Correctamente!',
                    });
                    this.idcategoria = "";
                    this.nombre = "";
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al eliminar la categoria!',
                    });
                    console.error("error al eliminar la categoria", error)
                });

        },
        listarCategorias() {
            axios
                .get("http://localhost:8080/api/categoria/listar")
                .then((response) => {
                    this.categorias = response.data;
                    this.contadorerrores = 0;
                })
                .catch((error) => {

                    this.contadorerrores++;

                    console.error("error al cargar categoria", error);
                    if (this.contadorerrores >= this.maxErrores) {
                        swal.fire({
                            icon: 'error',
                            title: 'Servidor no responde',
                            text: 'Demasiados errores al intentar conectar al servidor! No: ' + this.contadorerrores,
                        });

                    } else {
                        swal.fire({
                            icon: 'error',
                            title: 'Error',
                            text: 'Hubo un error al cargar categoria! No: ' + this.contadorerrores,
                        });

                    }
                })
                .finally(() => {

                    let tiempo = this.contadorerrores > 0 ? 30000 * this.contadorerrores : 30000;

                    if (this.contadorerrores < this.maxErrores) {
                        setTimeout(this.listarCategorias, tiempo);
                    }
                    else {
                        setTimeout(this.listarCategorias, tiempo);
                    }
                });

        },
    },
    mounted() {
        this.listarCategorias();
    }
};
</script>

<style scoped>
.titulo_tabla {
    margin: 5px auto;
    /* Centrar la tabla y dar espacio alrededor */
    padding: 5px;
    width: 100%;
    /* Ajusta la tabla al ancho del contenedor */
    max-width: 1000px;
    /* Limita el ancho máximo de la tabla */
    overflow-x: auto;
    /* Hace scroll horizontal si es necesario */
}

.table-container {
    margin: 20px auto;
    /* Centrar la tabla y dar espacio alrededor */
    padding: 10px;
    width: 100%;
    /* Ajusta la tabla al ancho del contenedor */
    max-width: 1200px;
    /* Limita el ancho máximo de la tabla */
    overflow-x: auto;
    /* Hace scroll horizontal si es necesario */
}

table {
    width: 100%;
    /* Usa todo el ancho disponible */
    border-collapse: collapse;
    /* Elimina espacios entre celdas */
    margin: 10px 0;
    /* Margen para separar la tabla de otros elementos */
    font-size: 16px;
    /* Tamaño de fuente ajustable */
    background-color: #F2F2F2;
    /* Color de fondo suave */
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    /* Sombra suave */
}

thead {
    background-color: #4F4050;
    /* Fondo de los encabezados */
    color: #ffffff;
    /* Color del texto en los encabezados */
}

th,
td {
    text-align: left;
    /* Alinear texto a la izquierda */
    padding: 12px 15px;
    /* Espacio interno en las celdas */
    border: 1px solid #ddd;
    /* Bordes suaves entre las celdas */
}

tr:nth-child(even) {
    background-color: #f2f2f2;
    /* Color para filas pares */
}

tr:hover {
    background-color: #A294A9;
    /* Color al pasar el mouse */
}

/*  Stilo para el formulario  */
.form-container {
    margin: 5px no;
    padding: 5px;
    width: 100%;
    max-width: 900px;
    background-color: #F2F2F2;
    /* Fondo blanco para el formulario */
    box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
    /* Sombra suave */
    border-radius: 10px;
    /* Bordes redondeados */
}

form {
    display: flex;
    flex-direction: column;
}

.form-group {
    margin-bottom: 5px;
}

label {
    display: block;
    margin-bottom: 1px;
    font-weight: bold;
    color: #4F4050;
    /* Color del texto */
}

input {
    width: 95%;
    padding: 5px;
    border: 1px solid #ddd;
    /* Borde suave */
    border-radius: 4px;
    /* Bordes redondeados para los campos de entrada */
    font-size: 16px;
}

input:focus {
    border-color: #4F4050;
    /* Borde al enfocar */
    outline: none;
    /* Eliminar el borde de enfoque predeterminado */
}

.form-actions {
    display: flex;
    justify-content: flex-end;
    gap: 15px;
}

.btn-submit,
.btn-crud {
    padding: 5px 5px;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
}

.btn-submit {
    background-color: #4F4050;
    /* Fondo de botón de guardar */
    color: #ffffff;
    /* Color de texto de botón de guardar */
}

.btn-submit:hover {
    background-color: #0F8B8D;
    /* Fondo al pasar el mouse */
}

.btn-crud {
    background-color: #4F4050;
    /* Fondo de botón de cancelar */
    color: #ffffff;
    /* Color de texto de botón de cancelar */
}

.btn-crud:hover {
    background-color: #0F8B8D;
    /* Fondo al pasar el mouse */
}


@media screen and (max-width: 768px) {
    table {
        font-size: 14px;
        /* Fuente más pequeña para pantallas pequeñas */
    }

    th,
    td {
        padding: 8px;
        /* Reducir padding en dispositivos pequeños */
    }
}
</style>