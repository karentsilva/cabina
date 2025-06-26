<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Agendar Cita - Cabina Cosmetológica</title>
  <style>
    body {
      background-color: #f6f4fb;
      font-family: 'Segoe UI', sans-serif;
      color: #333;
      padding: 20px;
    }
    .contenedor {
      max-width: 500px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 16px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    h2 {
      text-align: center;
      color: #633a82;
    }
    label {
      display: block;
      margin-top: 10px;
      font-weight: 500;
    }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border-radius: 8px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
    button {
      background-color: #a97ac3;
      color: white;
      font-weight: bold;
      cursor: pointer;
      border: none;
      margin-top: 20px;
    }
    #mensaje {
      margin-top: 15px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="contenedor">
    <h2>Agendar tu Cita</h2>
    <form id="formulario">
      <label>Nombre:</label>
      <input type="text" id="nombre" required>

      <label>Teléfono:</label>
      <input type="tel" id="telefono" required>

      <label>Hora (10:00 - 18:00):</label>
      <input type="time" id="hora" min="10:00" max="18:00" required>

      <label>Tratamiento:</label>
      <select id="tratamiento" required onchange="toggleZona()">
        <optgroup label="Faciales">
          <option>Limpieza facial profunda</option>
          <option>Radiofrecuencia facial</option>
          <option>Perfilado facial no invasivo</option>
          <option>Tratamiento despigmentante facial</option>
          <option>Dermapen facial</option>
        </optgroup>
        <optgroup label="Corporales">
          <option>Despigemntante corporal</option>
          <option>Dermapen corporal</option>
          <option>Cavitación</option>
          <option>Vacumterapia</option>
          <option>Lipoláser</option>
          <option>Gimnasia pasiva</option>
          <option>Copas colombianas</option>
        </optgroup>
      </select>

      <div id="zonaDiv" style="display: none;">
        <label>Zona del cuerpo:</label>
        <select id="zona">
          <option>Abdomen</option>
          <option>Piernas</option>
          <option>Glúteos</option>
          <option>Brazos</option>
          <option>Espalda</option>
          <option>Pecho</option>
          <option>Caderas</option>
        </select>
      </div>

      <button type="submit">Agendar cita</button>
      <p id="mensaje"></p>
    </form>
  </div>

  <script>
    const scriptURL = "https://script.google.com/macros/s/TU_URL_DEL_SCRIPT/exec"; // <-- REEMPLAZA AQUÍ

    document.getElementById("formulario").addEventListener("submit", function (e) {
      e.preventDefault();
      const datos = {
        nombre: document.getElementById("nombre").value,
        telefono: document.getElementById("telefono").value,
        hora: document.getElementById("hora").value,
        tratamiento: document.getElementById("tratamiento").value,
        zona: document.getElementById("zona")?.value || ""
      };

      fetch(scriptURL, {
        method: "POST",
        body: JSON.stringify(datos),
        headers: { "Content-Type": "application/json" }
      })
      .then(() => {
        document.getElementById("mensaje").innerText = "✅ Cita registrada correctamente.";
        document.getElementById("formulario").reset();
        document.getElementById("zonaDiv").style.display = "none";
      })
      .catch(() => {
        document.getElementById("mensaje").innerText = "❌ Error al registrar la cita.";
      });
    });

    function toggleZona() {
      const corporal = [
        "Despigemntante corporal", "Dermapen corporal", "Cavitación",
        "Vacumterapia", "Lipoláser", "Gimnasia pasiva", "Copas colombianas"
      ];
      const seleccion = document.getElementById("tratamiento").value;
      document.getElementById("zonaDiv").style.display = corporal.includes(seleccion) ? "block" : "none";
    }
  </script>
</body>
</html>
