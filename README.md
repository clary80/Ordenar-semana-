<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diario Casa</title>


<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f7f3ef;
  color: #4d4038;
}

header {
  background: #d9c2b0;
  padding: 22px 15px;
  text-align: center;
}

header h1 {
  margin: 0;
  font-size: 30px;
}

header p {
  margin: 8px 0 0;
}

nav {
  display: flex;
  justify-content: center;
  gap: 6px;
  flex-wrap: wrap;
  background: #fff;
  padding: 10px;
  box-shadow: 0 2px 8px rgba(0,0,0,.08);
  position: sticky;
  top: 0;
  z-index: 10;
}

nav button {
  background: #eaded5;
  color: #4d4038;
  padding: 10px 14px;
}

nav button.active {
  background: #b99780;
  color: white;
}

.container {
  max-width: 700px;
  margin: auto;
  padding: 15px;
}

.card {
  background: white;
  border-radius: 18px;
  padding: 20px;
  margin: 15px 0;
  box-shadow: 0 3px 12px rgba(0,0,0,.08);
}

.card h2 {
  margin-top: 0;
}

.item {
  padding: 12px;
  margin: 8px 0;
  background: #f4eee9;
  border-radius: 12px;
}

input,
select,
button {
  font-size: 16px;
  border-radius: 10px;
  padding: 10px;
}

input,
select {
  border: 1px solid #d5c5b9;
  width: 100%;
  margin-bottom: 10px;
  background: white;
  color: #4d4038;
}

button {
  border: none;
  background: #b99780;
  color: white;
  cursor: pointer;
}

button:hover {
  opacity: .9;
}

button.delete {
  background: #c98f82;
  padding: 7px 10px;
  font-size: 14px;
}

button.small {
  padding: 8px 12px;
  font-size: 14px;
}

.check {
  display: flex;
  align-items: center;
  gap: 10px;
}

.check input {
  width: auto;
  margin: 0;
}

.task {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px;
  margin: 8px 0;
  background: #f4eee9;
  border-radius: 12px;
}

.task.done {
  opacity: .6;
}

.task.done .task-name {
  text-decoration: line-through;
}

.task-info {
  flex: 1;
}

.task-time {
  font-weight: bold;
  color: #9a7861;
  min-width: 52px;
}

.task-name {
  font-size: 16px;
}

.task-category {
  font-size: 12px;
  color: #806f63;
  margin-top: 3px;
}

.add-form {
  background: #faf7f4;
  padding: 15px;
  border-radius: 14px;
  margin-top: 15px;
}

.add-form button {
  width: 100%;
}

.progress {
  background: #eee;
  border-radius: 20px;
  overflow: hidden;
  height: 18px;
  margin-top: 10px;
}

.progress-bar {
  width: 0%;
  height: 100%;
  background: #a98770;
  transition: width .3s;
}

.progress-text {
  margin-bottom: 5px;
  font-weight: bold;
}

.empty {
  text-align: center;
  color: #806f63;
  padding: 20px 5px;
}

.section {
  display: none;
}

.section.active {
  display: block;
}

.date-title {
  font-size: 18px;
  font-weight: bold;
  margin-top: 10px;
}

.summary {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}

.summary-box {
  background: #f4eee9;
  padding: 15px;
  border-radius: 14px;
  text-align: center;
}

.summary-number {
  font-size: 25px;
  font-weight: bold;
}

footer {
  text-align: center;
  padding: 25px;
  color: #806f63;
}

@media (max-width: 500px) {
  .task {
    align-items: flex-start;
  }

  .task-time {
    min-width: 45px;
  }

  nav button {
    font-size: 14px;
    padding: 9px 10px;
  }
}
</style>
</head>

<body>

<header>
  <h1>🏠 Diario Casa</h1>
  <p>Organiza tu día, tu casa y tu bienestar</p>
</header>

<nav>
  <button class="nav-btn active" data-section="inicio">🏠 Inicio</button>
  <button class="nav-btn" data-section="agenda">📅 Agenda</button>
  <button class="nav-btn" data-section="casa">🧹 Casa</button>
  <button class="nav-btn" data-section="bienestar">🌿 Bienestar</button>
</nav>

<div class="container">

  <!-- INICIO -->
  <section id="inicio" class="section active">

    <div class="card">
      <h2>📅 Mi día</h2>

      <input type="date" id="fechaInicio">

      <div class="date-title" id="inicioFechaTexto"></div>

      <div class="summary">
        <div class="summary-box">
          <div class="summary-number" id="inicioTotal">0</div>
          <div>Tareas</div>
        </div>

        <div class="summary-box">
          <div class="summary-number" id="inicioHechas">0</div>
          <div>Realizadas</div>
        </div>
      </div>

      <p class="progress-text" id="inicioProgresoTexto">
        Progreso: 0%
      </p>

      <div class="progress">
        <div class="progress-bar" id="inicioBarra"></div>
      </div>
    </div>

    <div class="card">
      <h2>💼 Horario de trabajo</h2>

      <div class="item">
        🚗 <strong>Traslado:</strong> 1 hora
      </div>

      <div class="item">
        💼 <strong>Trabajo:</strong> 10:00 a 16:00
      </div>
    </div>

    <div class="card">
      <h2>⏰ Próximas tareas</h2>
      <div id="inicioTareas"></div>
    </div>

  </section>


  <!-- AGENDA -->
  <section id="agenda" class="section">

    <div class="card">
      <h2>📅 Agenda</h2>

      <input type="date" id="fechaAgenda">

      <p id="agendaFechaTexto">
        Selecciona una fecha
      </p>

      <p class="progress-text" id="agendaProgresoTexto">
        Progreso: 0%
      </p>

      <div class="progress">
        <div class="progress-bar" id="agendaBarra"></div>
      </div>
    </div>

    <div class="card">
      <h2>➕ Agregar tarea</h2>

      <div class="add-form">

        <label>⏰ Horario</label>
        <input type="time" id="horaTarea">

        <label>📝 Tarea</label>
        <input
          type="text"
          id="nombreTarea"
          placeholder="Ej.: Limpiar cocina"
        >

        <label>📂 Categoría</label>
        <select id="categoriaTarea">
          <option value="Casa">🏠 Casa</option>
          <option value="Bienestar">🌿 Bienestar</option>
          <option value="Trabajo">💼 Trabajo</option>
          <option value="Personal">✨ Personal</option>
        </select>

        <button id="agregarTarea">
          ➕ Agregar tarea
        </button>

      </div>
    </div>

    <div class="card">
      <h2>📋 Tareas del día</h2>

      <div id="listaTareas"></div>
    </div>

  </section>


  <!-- CASA -->
  <section id="casa" class="section">

    <div class="card">
      <h2>🏠 Casa</h2>

      <p>
        Estas tareas se pueden agregar a la fecha que elijas
        desde la Agenda.
      </p>

      <div class="item">
        🛏️ Ordenar las 2 camas
      </div>

      <div class="item">
        🛁 Limpiar el baño
      </div>

      <div class="item">
        🍳 Ordenar y limpiar la cocina
      </div>

      <div class="item">
        🍽️ Ordenar comedor
      </div>

      <div class="item">
        📺 Ordenar mueble del televisor
      </div>

      <div class="item">
        💻 Ordenar escritorio
      </div>

      <div class="item">
        🧹 Barrer y limpiar el piso
      </div>

      <div class="item">
        🧺 Guardar ropa y objetos
      </div>

      <button id="agregarCasa">
        ➕ Agregar tarea de casa para este día
      </button>
    </div>

  </section>


  <!-- BIENESTAR -->
  <section id="bienestar" class="section">

    <div class="card">
      <h2>🌿 Bienestar</h2>

      <div class="item">
        🚿 Ducha
      </div>

      <div class="item">
        🪥 Higiene dental
      </div>

      <div class="item">
        🧴 Cuidado de la piel
      </div>

      <div class="item">
        💇 Cuidado del cabello
      </div>

      <div class="item">
        💧 Tomar agua
      </div>

      <div class="item">
        😴 Prepararse para descansar
      </div>

      <div class="item">
        🏋️ Preparar ropa y bolso
      </div>

      <div class="item">
        🏋️ Entrenamiento realizado
      </div>

      <div class="item">
        🧘 Estiramiento
      </div>

      <button id="agregarBienestar">
        ➕ Agregar tarea de bienestar para este día
      </button>
    </div>

  </section>

</div>

<footer>
  💕 Mi día, mi casa, mi bienestar
</footer>


<script>

/* =========================================================
   DIARIO CASA
   Datos separados por fecha y guardados en el celular
========================================================= */

const STORAGE_KEY = "diarioCasaTareasV2";

let datos = cargarDatos();

const fechaInicio = document.getElementById("fechaInicio");
const fechaAgenda = document.getElementById("fechaAgenda");

const hoy = obtenerFechaHoy();

fechaInicio.value = hoy;
fechaAgenda.value = hoy;


/* =========================================================
   FUNCIONES DE FECHA
========================================================= */

function obtenerFechaHoy() {
  const ahora = new Date();

  const año = ahora.getFullYear();
  const mes = String(ahora.getMonth() + 1).padStart(2, "0");
  const dia = String(ahora.getDate()).padStart(2, "0");

  return `${año}-${mes}-${dia}`;
}

function fechaBonita(fecha) {

  if (!fecha) return "";

  const partes = fecha.split("-");

  return `${partes[2]}/${partes[1]}/${partes[0]}`;
}


/* =========================================================
   GUARDAR / CARGAR
========================================================= */

function cargarDatos() {

  try {

    const guardado = localStorage.getItem(STORAGE_KEY);

    if (guardado) {
      return JSON.parse(guardado);
    }

  } catch (error) {
    console.log("No se pudieron cargar los datos.");
  }

  return {};
}


function guardarDatos() {

  try {

    localStorage.setItem(
      STORAGE_KEY,
      JSON.stringify(datos)
    );

  } catch (error) {

    alert(
      "No se pudieron guardar los datos en el celular."
    );

  }
}


function obtenerTareas(fecha) {

  if (!datos[fecha]) {
    datos[fecha] = [];
  }

  return datos[fecha];
}


/* =========================================================
   ORDENAR TAREAS
========================================================= */

function ordenarTareas(tareas) {

  tareas.sort((a, b) => {

    const horaA = a.hora || "23:59";
    const horaB = b.hora || "23:59";

    return horaA.localeCompare(horaB);

  });

}


/* =========================================================
   AGREGAR TAREA
========================================================= */

function agregarNuevaTarea() {

  const fecha = fechaAgenda.value;
  const hora = document.getElementById("horaTarea").value;
  const nombre = document.getElementById("nombreTarea").value.trim();
  const categoria = document.getElementById("categoriaTarea").value;

  if (!fecha) {

    alert("Primero seleccioná una fecha.");

    return;
  }

  if (!nombre) {

    alert("Escribí el nombre de la tarea.");

    return;
  }

  if (!hora) {

    alert("Elegí un horario.");

    return;
  }

  const tareas = obtenerTareas(fecha);

  tareas.push({

    id: Date.now(),

    hora: hora,

    nombre: nombre,

    categoria: categoria,

    hecha: false

  });

  ordenarTareas(tareas);

  guardarDatos();

  document.getElementById("nombreTarea").value = "";
  document.getElementById("horaTarea").value = "";

  mostrarAgenda();
  actualizarInicio();

}


/* =========================================================
   MOSTRAR AGENDA
========================================================= */

function mostrarAgenda() {

  const fecha = fechaAgenda.value;

  const lista = document.getElementById("listaTareas");
  const texto = document.getElementById("agendaFechaTexto");

  texto.textContent =
    fecha
      ? "Fecha seleccionada: " + fechaBonita(fecha)
      : "Selecciona una fecha";

  lista.innerHTML = "";

  if (!fecha) {

    lista.innerHTML =
      '<div class="empty">Seleccioná una fecha.</div>';

    actualizarProgresoAgenda();

    return;
  }

  const tareas = obtenerTareas(fecha);

  ordenarTareas(tareas);

  if (tareas.length === 0) {

    lista.innerHTML =
      '<div class="empty">No hay tareas para este día. ➕ Agregá una tarea.</div>';

  } else {

    tareas.forEach(tarea => {

      const elemento = document.createElement("div");

      elemento.className =
        "task" + (tarea.hecha ? " done" : "");

      elemento.innerHTML = `

        <input
          type="checkbox"
          ${tarea.hecha ? "checked" : ""}
          aria-label="Marcar tarea realizada"
        >

        <div class="task-time">
          ${tarea.hora}
        </div>

        <div class="task-info">

          <div class="task-name">
            ${escapeHTML(tarea.nombre)}
          </div>

          <div class="task-category">
            ${escapeHTML(tarea.categoria)}
          </div>

        </div>

        <button
          class="delete"
          title="Eliminar tarea"
        >
          🗑️
        </button>
      `;


      const checkbox =
        elemento.querySelector("input[type='checkbox']");

      checkbox.addEventListener("change", function() {

        tarea.hecha = this.checked;

        guardarDatos();

        mostrarAgenda();
        actualizarInicio();

      });


      const botonEliminar =
        elemento.querySelector(".delete");

      botonEliminar.addEventListener("click", function() {

        eliminarTarea(fecha, tarea.id);

      });


      lista.appendChild(elemento);

    });

  }

  actualizarProgresoAgenda();

}


function eliminarTarea(fecha, id) {

  if (!confirm("¿Eliminar esta tarea?")) {
    return;
  }

  datos[fecha] =
    obtenerTareas(fecha).filter(
      tarea => tarea.id !== id
    );

  guardarDatos();

  mostrarAgenda();
  actualizarInicio();

}


/* =========================================================
   PROGRESO
========================================================= */

function calcularProgreso(fecha) {

  const tareas = obtenerTareas(fecha);

  const total = tareas.length;

  const hechas =
    tareas.filter(tarea => tarea.hecha).length;

  const porcentaje =
    total === 0
      ? 0
      : Math.round((hechas / total) * 100);

  return {
    total,
    hechas,
    porcentaje
  };

}


function actualizarProgresoAgenda() {

  const resultado =
    calcularProgreso(fechaAgenda.value);

  document.getElementById(
    "agendaProgresoTexto"
  ).textContent =
    `Progreso: ${resultado.porcentaje}%`;

  document.getElementById(
    "agendaBarra"
  ).style.width =
    resultado.porcentaje + "%";

}


/* =========================================================
   INICIO
========================================================= */

function actualizarInicio() {

  const fecha = fechaInicio.value;

  const resultado =
    calcularProgreso(fecha);

  document.getElementById(
    "inicioFechaTexto"
  ).textContent =
    fecha
      ? "Fecha: " + fechaBonita(fecha)
      : "Seleccioná una fecha";

  document.getElementById(
    "inicioTotal"
  ).textContent =
    resultado.total;

  document.getElementById(
    "inicioHechas"
  ).textContent =
    resultado.hechas;

  document.getElementById(
    "inicioProgresoTexto"
  ).textContent =
    `Progreso: ${resultado.porcentaje}%`;

  document.getElementById(
    "inicioBarra"
  ).style.width =
    resultado.porcentaje + "%";


  mostrarProximasTareas(fecha);

}


function mostrarProximasTareas(fecha) {

  const contenedor =
    document.getElementById("inicioTareas");

  contenedor.innerHTML = "";

  const tareas =
    [...obtenerTareas(fecha)];

  ordenarTareas(tareas);

  const pendientes =
    tareas.filter(tarea => !tarea.hecha);

  if (pendientes.length === 0) {

    contenedor.innerHTML =
      '<div class="empty">🎉 No tenés tareas pendientes para este día.</div>';

    return;
  }

  pendientes.slice(0, 5).forEach(tarea => {

    const elemento =
      document.createElement("div");

    elemento.className = "item";

    elemento.innerHTML = `
      ⏰ <strong>${tarea.hora}</strong>
      — ${escapeHTML(tarea.nombre)}
    `;

    contenedor.appendChild(elemento);

  });

}


/* =========================================================
   BOTONES DE CASA Y BIENESTAR
========================================================= */

function agregarTareaRapida(nombre, categoria) {

  const fecha = fechaInicio.value || hoy;

  const hora =
    prompt(
      `¿A qué hora querés hacer "${nombre}"?`,
      "08:00"
    );

  if (hora === null) {
    return;
  }

  if (!/^\d{2}:\d{2}$/.test(hora)) {

    alert("Ingresá una hora válida, por ejemplo 08:30.");

    return;
  }

  const tareas = obtenerTareas(fecha);

  tareas.push({

    id: Date.now(),

    hora: hora,

    nombre: nombre,

    categoria: categoria,

    hecha: false

  });

  ordenarTareas(tareas);

  guardarDatos();

  actualizarInicio();

  if (fechaAgenda.value === fecha) {
    mostrarAgenda();
  }

}


/* =========================================================
   SEGURIDAD PARA TEXTO INGRESADO POR EL USUARIO
========================================================= */

function escapeHTML(texto) {

  const div = document.createElement("div");

  div.textContent = texto;

  return div.innerHTML;

}


/* =========================================================
   NAVEGACIÓN
========================================================= */

document.querySelectorAll(".nav-btn")
.forEach(boton => {

  boton.addEventListener("click", function() {

    const seccion =
      this.dataset.section;

    document.querySelectorAll(".nav-btn")
    .forEach(btn => {
      btn.classList.remove("active");
    });

    this.classList.add("active");


    document.querySelectorAll(".section")
    .forEach(sec => {
      sec.classList.remove("active");
    });

    document
      .getElementById(seccion)
      .classList.add("active");


    if (seccion === "agenda") {
      mostrarAgenda();
    }

    if (seccion === "inicio") {
      actualizarInicio();
    }

  });

});


/* =========================================================
   EVENTOS DE FECHA
========================================================= */

fechaAgenda.addEventListener(
  "change",
  mostrarAgenda
);

fechaInicio.addEventListener(
  "change",
  actualizarInicio
);


/* =========================================================
   AGREGAR TAREA
========================================================= */

document
  .getElementById("agregarTarea")
  .addEventListener(
    "click",
    agregarNuevaTarea
  );


document
  .getElementById("agregarCasa")
  .addEventListener(
    "click",
    function() {

      const nombre =
        prompt(
          "¿Qué tarea de casa querés agregar?"
        );

      if (nombre && nombre.trim()) {

        agregarTareaRapida(
          nombre.trim(),
          "Casa"
        );

      }

    }
  );


document
  .getElementById("agregarBienestar")
  .addEventListener(
    "click",
    function() {

      const nombre =
        prompt(
          "¿Qué tarea de bienestar querés agregar?"
        );

      if (nombre && nombre.trim()) {

        agregarTareaRapida(
          nombre.trim(),
          "Bienestar"
        );

      }

    }
  );


/* =========================================================
   INICIO DE LA APLICACIÓN
========================================================= */

actualizarInicio();
mostrarAgenda();

</script>

</body>
</html>
