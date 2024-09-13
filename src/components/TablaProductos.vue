<template>
    <div>
        <div class="titulo_tabla">
            <h3>Productos</h3>
        </div>
    </div>

    <div>
        <form class="form-container">
            <div class="form-group">
                <label for="txtId">ID:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtId" name="IdProducto" />
            </div>
            <div class="form-group">
                <label for="txtNombre">Nombre:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtNombre" name="nombreProducto" />
            </div>
            <div class="form-group">
                <label for="numPrecio">Precio:</label><!-- Etiqueta para escritura -->
                <input type="number" id="numPrecio" name="PrecioProducto" />
            </div>
            <div class="form-group">
                <label for="numCant">Cantidad:</label><!-- Etiqueta para escritura -->
                <input type="number" id="numCant" name="Cantidad" />
            </div>
            <div class="form-group">
                <label for="txtProveedor">Proveedor:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtProveedor" name="Proveedor" />
            </div>
            <div class="form-group">
                <label for="txtCategoria">Categoria:</label><!-- Etiqueta para escritura -->
                <input type="text" id="txtCategoria" name="Categoria" />
            </div>
            <div class="form-group">
                <label for="numCosto">Costo:</label><!-- Etiqueta para escritura -->
                <input type="number" id="numCosto" name="CostoProducto" />
            </div>
            <div class="form-actions">
                <button type="submit" id="guardarProducto" name="guardarProducto" class="btn-submit">Registrar</button>
                <button type="submit" class="btn-crud">Buscar</button>
                <button type="button" class="btn-crud">Eliminar</button>
                <button type="button" class="btn-crud">Actualizar</button>
            </div>
        </form>

    </div>

    <div>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th> Id </th>
                        <th> Nombre </th>
                        <th> Precio </th>
                        <th> Cantidad </th>
                        <th> Proveedor </th>
                        <th> Categoria </th>
                        <th> Costo </th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>dato # 1.</td>
                        <td>Dato # 2</td>
                        <td>d4tos # 3</td>
                        <td>D4t3 # 5</td>
                        <td>Dato # 2</td>
                        <td>d4tos # 3</td>
                        <td>D4t3 # 5</td>
                    </tr>
                    <tr>
                        <td>1 # date</td>
                        <td> Dato 2</td>
                        <td>dato 3</td>
                        <td>cuarta celda.</td>
                        <td>Dato # 2</td>
                        <td>d4tos # 3</td>
                        <td>D4t3 # 5</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {

    data() {

        return {
            idProducto: "",
            nombre: "",
            PrecioVenta: "",
            cantidad: "",
            Proveedor: "",
            Categoria: "",
            costoProducto: "",

        };
    },

    methods: {
        async getData() {
            const response = await axios.get('dominio.com.co');
            console.log(response.data)
        }
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

table {
    width: 100%;
    /* Usa todo el ancho disponible */
    border-collapse: collapse;
    /* Elimina espacios entre celdas */
    margin: 5px 0;
    /* Margen para separar la tabla de otros elementos */
    font-size: 16px;
    /* Tamaño de fuente ajustable */
    background-color: #F2F2F2;
    /* Color de fondo suave */
    box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
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