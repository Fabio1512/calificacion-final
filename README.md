<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Calculadora de Calificación Final</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <!-- Bootstrap -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" />
  <!-- SweetAlert2 -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
</head>
<body class="bg-light">

  <div class="container mt-5">
    <div class="card shadow">
      <div class="card-body">
        <h2 class="card-title text-center mb-4">Calificación Final del Estudiante</h2>
        <form id="formulario">
          <div class="mb-3">
            <label for="nota1" class="form-label">Nota del 1.er Parcial (máx. 30):</label>
            <input type="number" class="form-control" id="nota1" placeholder="Ej: 25" min="0" max="30" />
          </div>
          <div class="mb-3">
            <label for="nota2" class="form-label">Nota del 2.º Parcial (máx. 30):</label>
            <input type="number" class="form-control" id="nota2" placeholder="Ej: 28" min="0" max="30" />
          </div>
          <div class="mb-3">
            <label for="nota3" class="form-label">Nota del 3.er Parcial (máx. 40):</label>
            <input type="number" class="form-control" id="nota3" placeholder="Ej: 35" min="0" max="40" />
          </div>
          <div class="mb-3">
            <label for="resultado" class="form-label">Calificación Final:</label>
            <input type="text" class="form-control" id="resultado" readonly />
          </div>
          <div class="mb-3">
            <label for="mensaje" class="form-label">Mensaje:</label>
            <input type="text" class="form-control" id="mensaje" readonly />
          </div>
          <div class="d-flex justify-content-between">
            <button type="button" class="btn btn-success" onclick="calcularCalificacion()">Calcular</button>
            <button type="button" class="btn btn-secondary" onclick="limpiarFormulario()">Limpiar</button>
          </div>
        </form>
      </div>
    </div>
  </div>

  <script>
    function calcularCalificacion() {
      const nota1 = document.getElementById("nota1").value.trim();
      const nota2 = document.getElementById("nota2").value.trim();
      const nota3 = document.getElementById("nota3").value.trim();

      if (nota1 === "" || nota2 === "" || nota3 === "") {
        Swal.fire("Error", "Todos los campos deben estar completos.", "error");
        return;
      }

      if (isNaN(nota1) || isNaN(nota2) || isNaN(nota3)) {
        Swal.fire("Error", "Todos los valores deben ser números.", "error");
        return;
      }

      const n1 = parseFloat(nota1);
      const n2 = parseFloat(nota2);
      const n3 = parseFloat(nota3);

      if (n1 < 0 || n1 > 30) {
        Swal.fire("Error", "La nota del 1.er Parcial debe estar entre 0 y 30.", "error");
        return;
      }

      if (n2 < 0 || n2 > 30) {
        Swal.fire("Error", "La nota del 2.º Parcial debe estar entre 0 y 30.", "error");
        return;
      }

      if (n3 < 0 || n3 > 40) {
        Swal.fire("Error", "La nota del 3.er Parcial debe estar entre 0 y 40.", "error");
        return;
      }

      const total = n1 + n2 + n3;
      let mensaje = "";

      if (total < 60) mensaje = "Reprobado";
      else if (total < 80) mensaje = "Bueno";
      else if (total < 90) mensaje = "Muy Bueno";
      else mensaje = "Sobresaliente";

      document.getElementById("resultado").value = total.toFixed(2);
      document.getElementById("mensaje").value = mensaje;

      Swal.fire("Éxito", `Calificación final: ${total} - ${mensaje}`, "success");
    }

    function limpiarFormulario() {
      document.getElementById("formulario").reset();
      document.getElementById("resultado").value = "";
      document.getElementById("mensaje").value = "";
    }
  </script>

</body>
</html>
