<template>

    <div>
        <div class="titulo_tabla">
            <h3>Proveedores</h3>
        </div>
    </div>
    <form class="form-container" @submit.prevent="guardar">
        <div>
            <div class="form-group">
                <label for="txtId">ID Proveedor:</label><!-- Etiqueta para escritura -->
                <input type="number" id="txtId" name="IdProveedor" v-model="idProveedor" required />
            </div>

            <div class="form-group">
                <label for="txtNombre">Nombre:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtNombre" name="nombreProveedor" v-model="nombre" required />
            </div>

            <div class="form-group">
                <label for="txtTelefono">Telefono:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtTelefono" name="telefonoProveedor" v-model="telefono" required />
            </div>

            <div class="form-group">
                <label for="txtCorreo">Correo:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtCorreo" name="correoProveedor" v-model="correo" required />
            </div>

            <div class="form-group">
                <label for="txtHorarios">Horarios:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtHorarios" name="horarioProveedor" v-model="horario" />
            </div>

            <div class="form-group">
                <label for="txtDireccion">Direccion:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtDireccion" name="direccionProveedor" v-model="direccion" />
            </div>
            <div class="form-group">
                <label for="txtpaginaWeb">PaginaWeb:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtPaginaWeb" name="PaginaWebProveedor" v-model="paginaWeb" />
            </div>
            <div class="form-group">
                <label for="txtCiudad">Ciudad:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtCiudad" name="ciudadProveedor" v-model="ciudad" required />
            </div>
            <div class="form-actions">
                <button type="submit" id="guardarProveedor" name="guardarProveedor"
                    class="btn-submit">Registrar</button>
                <button type="submit" class="btn-crud" name="consultar" id="consultar"
                    @click="consultar">Consultar</button> <!-- Boton para Busar Proveedor -->
                <button type="button" class="btn-crud" name="eliminar" id="eliminar" @click="eliminar">Eliminar</button>
                <!-- Boton para Borrar un Proveedor -->
                <button type="button" class="btn-crud" name="actualizar" id="actualizar"
                    @click="actualizar">Actualizar</button> <!-- Boton para Actualizar Proveedor -->
            </div>
        </div>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th> Id </th>
                        <th> Nombre </th>
                        <th> Teléfono </th>
                        <th> Correo </th>
                        <th> Horario </th>
                        <th> Dirección </th>
                        <th> Pagina Web </th>
                        <th> Ciudad </th>
                    </tr>
                </thead>
                <tr v-for="proveedor in proveedores" :key="proveedor.idProveedor">
                    <td>{{ proveedor.idProveedor }}</td>
                    <td>{{ proveedor.nombre }}</td>
                    <td>{{ proveedor.telefono }}</td>
                    <td>{{ proveedor.correo }}</td>
                    <td>{{ proveedor.horario }}</td>
                    <td>{{ proveedor.direccion }}</td>
                    <td>{{ proveedor.paginaWeb }}</td>
                    <td>{{ proveedor.ciudad }}</td>
                </tr>
            </table>
        </div>
    </form>

</template>

<script>
import axios from 'axios';
import swal from 'sweetalert2'

export default {
    data() {
        return {
            proveedores: [],
            idProveedor: "",
            nombre: "",
            telefono: "",
            correo: "",
            horario: "",
            direccion: "",
            paginaWeb: "",
            ciudad: "",
            contadorerrores: 0,
            maxErrores: 5,
        };
    },
    methods: {
        guardar() {

            if (this.nombre.trim() === "") {
                swal.fire({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Nombre del Proveedor no puede estar vacío!',
                });
                return;
            }
            axios
                .post("http://localhost:8080/api/proveedor", {

                    idProveedor: this.idProveedor,
                    nombre: this.nombre,
                    telefono: this.telefono,
                    correo: this.correo,
                    horario: this.horario,
                    direccion: this.direccion,
                    paginaWeb: this.paginaWeb,
                    ciudad: this.ciudad,
                })
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Proveedor resgitrado',
                        text: 'El Proveedor: ' + response.data.nombre + ' ha sido registrado correctamente!',
                    });

                    this.idProveedor = "";
                    this.nombre = "";
                    this.telefono = "";
                    this.correo = "";
                    this.horario = "";
                    this.direccion = "";
                    this.paginaWeb = "";
                    this.ciudad = "";
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al registrar el proveedor!',
                    });
                    console.error("errror al registrar proveedor", error)
                });
        },
        consultar() {
            axios
                .get("http://localhost:8080/api/proveedor/" + this.idProveedor)
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Id valido',
                        text: 'Proveedor: ' + response.data.idCategoria + 'encontrado correctamente!',
                    });
                    this.nombre = response.data.nombre;
                    this.telefono = response.data.telefono;
                    this.correo = response.data.correo;
                    this.horario = response.data.horario;
                    this.direccion = response.data.direccion;
                    this.paginaWeb = response.data.paginaWeb;
                    this.ciudad = response.data.ciudad;
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al Listar el Id de el proveedor!',
                    });
                    console.error("errror al Consultar el Id del proveedor", error)
                });
        },
        actualizar() {
            axios
                .put("http://localhost:8080/api/proveedor/Actualizar/" + this.idProveedor, {

                    idProveedor: this.idProveedor,
                    nombre: this.nombre,
                    telefono: this.telefono,
                    correo: this.correo,
                    horario: this.horario,
                    direccion: this.direccion,
                    paginaWeb: this.paginaWeb,
                    ciudad: this.ciudad,
                })
                .then((response) => {
                    swal.fire({
                        icon: 'success',
                        title: 'Actualizacion Realizada',
                        text: 'Proveedor: ' + response.data.nombre + ' actualizado correctamente!',
                    });

                    this.nombre = "";
                    this.telefono = "";
                    this.correo = "";
                    this.horario = "";
                    this.direccion = "";
                    this.paginaWeb = "";
                    this.ciudad = "";

                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error actualizar la Proveedor!',
                    });
                    console.error("errror al actualizar la proveedor", error)
                });
        },
        eliminar() {
            axios
                .delete("http://localhost:8080/api/proveedor/" + this.idcategoria)
                .then(() => {
                    swal.fire({
                        icon: 'success',
                        title: 'Proveedor eliminada',
                        text: 'Proveedor Eliminada Correctamente!',
                    });
                    this.nombre = "";
                    this.telefono = "";
                    this.correo = "";
                    this.horario = "";
                    this.direccion = "";
                    this.paginaWeb = "";
                    this.ciudad = "";
                })
                .catch((error) => {
                    swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: 'Hubo un error al eliminar el proveedor!',
                    });
                    console.error("error al eliminar el proveedor", error)
                });

        },
        listarProveedor() {
            axios
                .get("http://localhost:8080/api/proveedor/listar")
                .then((response) => {
                    this.proveedores = response.data;
                    this.contadorerrores = 0;
                })
                .catch((error) => {

                    this.contadorerrores++;

                    console.error("error al cargar Proveedor", error);
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
                            text: 'Hubo un error al cargar proveedor! No: ' + this.contadorerrores,
                        });

                    }
                })
                .finally(() => {

                    let tiempo = this.contadorerrores > 0 ? 30000 * this.contadorerrores : 30000;

                    if (this.contadorerrores < this.maxErrores) {
                        setTimeout(this.listarProveedor, tiempo);
                    }
                    else {
                        setTimeout(this.listarProveedor, tiempo);
                    }
                });

        },
    },
    mounted() {
        this.listarProveedor();
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

th,
td {
    text-align: left;
    /* Alinear texto a la izquierda */
    padding: 12px 15px;
    /* Espacio interno en las celdas */
    border: 1px solid #ddd;
    /* Bordes suaves entre las celdas */
}

th {
    background-color: #4F4050;
    /* Fondo de los encabezados */
    color: white;
    /* Color de texto para los encabezados */
    text-transform: uppercase;
    /* Texto en mayúsculas */
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