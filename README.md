# Tarea-N-5-Laboratorio-Equipo
Tarea de Programación II

<!DOCTYPE html>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de Productos</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
</head>
<body class="container mt-4">
    <h2 class="text-center">Gestión de Productos</h2>
    
    <form id="productoForm" class="mb-4">
        <div class="row">
            <div class="col-md-3">
                <input type="text" id="productoId" class="form-control" placeholder="ID del Producto" required>
            </div>
            <div class="col-md-3">
                <input type="text" id="productoNombre" class="form-control" placeholder="Nombre del Producto" required>
            </div>
            <div class="col-md-2">
                <input type="number" id="productoPrecio" class="form-control" placeholder="Precio" required>
            </div>
            <div class="col-md-2">
                <input type="number" id="productoCantidad" class="form-control" placeholder="Cantidad" required>
            </div>
            <div class="col-md-2">
                <button type="button" class="btn btn-primary w-100" onclick="agregarProducto()">
                    <i class="fas fa-plus"></i> Agregar Producto
                </button>
            </div>
        </div>
    </form>

    <table class="table table-bordered text-center">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Precio</th>
                <th>Cantidad</th>
                <th>SubTotal</th>
            </tr>
        </thead>
        <tbody id="tablaProductos"></tbody>
    </table>

    <div class="row mt-3">
        <div class="col-md-3">
            <label>SubTotal:</label>
            <input type="text" id="subTotal" class="form-control" readonly>
        </div>
        <div class="col-md-3">
            <label>Descuento (10%):</label>
            <input type="text" id="descuento" class="form-control" readonly>
        </div>
        <div class="col-md-3">
            <label>ISV (15%):</label>
            <input type="text" id="isv" class="form-control" readonly>
        </div>
        <div class="col-md-3">
            <label>Total a Pagar:</label>
            <input type="text" id="totalPagar" class="form-control" readonly>
        </div>
    </div>

    <script>
        let subTotalGeneral = 0;
        function agregarProducto() {
            let id = document.getElementById("productoId").value;
            let nombre = document.getElementById("productoNombre").value;
            let precio = parseFloat(document.getElementById("productoPrecio").value);
            let cantidad = parseInt(document.getElementById("productoCantidad").value);
            
            if (!id || !nombre || isNaN(precio) || isNaN(cantidad) || cantidad <= 0 || precio <= 0) {
                alert("Por favor ingrese valores válidos.");
                return;
            }
            
            let subTotal = precio * cantidad;
            subTotalGeneral += subTotal;
            
            let fila = `<tr>
                            <td>${id}</td>
                            <td>${nombre}</td>
                            <td>${precio.toFixed(2)}</td>
                            <td>${cantidad}</td>
                            <td>${subTotal.toFixed(2)}</td>
                        </tr>`;
            document.getElementById("tablaProductos").innerHTML += fila;
            
            actualizarTotales();
            document.getElementById("productoForm").reset();
        }

        function actualizarTotales() {
            let descuento = subTotalGeneral * 0.10;
            let isv = subTotalGeneral * 0.15;
            let totalPagar = subTotalGeneral - descuento + isv;

            document.getElementById("subTotal").value = subTotalGeneral.toFixed(2);
            document.getElementById("descuento").value = descuento.toFixed(2);
            document.getElementById("isv").value = isv.toFixed(2);
            document.getElementById("totalPagar").value = totalPagar.toFixed(2);
        }
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
