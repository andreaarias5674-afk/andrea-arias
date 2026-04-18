<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Sistema CETAC 12 Avanzado</title>

<style>
body {margin:0;font-family:Arial;background:#eef2f7;}
#login {text-align:center;margin-top:100px;}
input {padding:8px;margin:5px;}
button {padding:8px 12px;background:#003366;color:white;border:none;cursor:pointer;}

.sidebar {
    width:220px;height:100vh;background:#002b5c;
    position:fixed;color:white;
}
.sidebar h2 {text-align:center;}
.sidebar button {
    width:100%;background:none;color:white;
    text-align:left;padding:12px;
}
.sidebar button:hover {background:#004080;}

.main {margin-left:220px;padding:20px;}

.card {
    background:white;padding:20px;margin:10px 0;
    border-radius:10px;
}

table {width:100%;border-collapse:collapse;}
td,th {border:1px solid #ccc;padding:8px;text-align:center;}

.seccion {display:none;}
.activa {display:block;}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="login">
    <h2>Sistema CETAC 12</h2>
    <input id="usuario" placeholder="Usuario"><br>
    <input id="password" type="password" placeholder="Contraseña"><br>
    <button onclick="entrar()">Ingresar</button>
</div>

<!-- APP -->
<div id="app" style="display:none;">

<div class="sidebar">
    <h2>CETAC 12</h2>
    <button onclick="mostrar('dashboard')">Inicio</button>
    <button onclick="mostrar('registro')">Registrar</button>
    <button onclick="mostrar('lista')">Alumnos</button>
    <button onclick="mostrar('calificaciones')">Calificaciones</button>
</div>

<div class="main">

<!-- DASHBOARD -->
<div id="dashboard" class="seccion activa">
    <div class="card">
        <h2>Panel Principal</h2>
        <p>Sistema escolar con gestión completa</p>
    </div>
</div>

<!-- REGISTRO -->
<div id="registro" class="seccion">
    <div class="card">
        <h2>Registrar Alumno</h2>
        <input id="nombre" placeholder="Nombre">
        <input id="grupo" placeholder="Grupo">
        <button onclick="registrar()">Guardar</button>
    </div>
</div>

<!-- LISTA -->
<div id="lista" class="seccion">
    <div class="card">
        <h2>Lista de Alumnos</h2>
        <table id="tablaAlumnos"></table>
    </div>
</div>

<!-- CALIFICACIONES -->
<div id="calificaciones" class="seccion">
    <div class="card">
        <h2>Agregar Calificación</h2>
        <input id="alumnoCal" placeholder="Nombre">
        <input id="calificacion" placeholder="Calificación">
        <button onclick="guardarCalificacion()">Guardar</button>
    </div>

    <div class="card">
        <h2>Calificaciones</h2>
        <table id="tablaCalificaciones"></table>
    </div>
</div>

</div>
</div>

<script>

// LOGIN
function entrar(){
    let u=document.getElementById("usuario").value;
    let p=document.getElementById("password").value;

    if(u==="admin" && p==="1234"){
        login.style.display="none";
        app.style.display="block";
        cargarAlumnos();
        cargarCalificaciones();
    } else alert("Error");
}

// NAVEGACIÓN
function mostrar(sec){
    document.querySelectorAll(".seccion").forEach(s=>s.classList.remove("activa"));
    document.getElementById(sec).classList.add("activa");
}

// REGISTRAR
function registrar(){
    let nombre=document.getElementById("nombre").value;
    let grupo=document.getElementById("grupo").value;

    let alumnos=JSON.parse(localStorage.getItem("alumnos"))||[];
    alumnos.push({nombre,grupo});
    localStorage.setItem("alumnos",JSON.stringify(alumnos));

    cargarAlumnos();
    alert("Alumno agregado");
}

// MOSTRAR ALUMNOS + EDITAR + ELIMINAR
function cargarAlumnos(){
    let tabla=document.getElementById("tablaAlumnos");
    let alumnos=JSON.parse(localStorage.getItem("alumnos"))||[];

    tabla.innerHTML="<tr><th>Nombre</th><th>Grupo</th><th>Acciones</th></tr>";

    alumnos.forEach((a,i)=>{
        tabla.innerHTML+=`
        <tr>
        <td>${a.nombre}</td>
        <td>${a.grupo}</td>
        <td>
        <button onclick="editar(${i})">Editar</button>
        <button onclick="eliminar(${i})">Eliminar</button>
        </td>
        </tr>`;
    });
}

// EDITAR
function editar(i){
    let alumnos=JSON.parse(localStorage.getItem("alumnos"));
    let nuevoNombre=prompt("Nuevo nombre:", alumnos[i].nombre);
    let nuevoGrupo=prompt("Nuevo grupo:", alumnos[i].grupo);

    if(nuevoNombre && nuevoGrupo){
        alumnos[i]={nombre:nuevoNombre,grupo:nuevoGrupo};
        localStorage.setItem("alumnos",JSON.stringify(alumnos));
        cargarAlumnos();
    }
}

// ELIMINAR
function eliminar(i){
    let alumnos=JSON.parse(localStorage.getItem("alumnos"));
    alumnos.splice(i,1);
    localStorage.setItem("alumnos",JSON.stringify(alumnos));
    cargarAlumnos();
}

// CALIFICACIONES
function guardarCalificacion(){
    let nombre=document.getElementById("alumnoCal").value;
    let cal=parseFloat(document.getElementById("calificacion").value);

    let calificaciones=JSON.parse(localStorage.getItem("calificaciones"))||[];
    calificaciones.push({nombre,cal});
    localStorage.setItem("calificaciones",JSON.stringify(calificaciones));

    cargarCalificaciones();
}

// MOSTRAR CALIFICACIONES + PROMEDIO + ELIMINAR
function cargarCalificaciones(){
    let tabla=document.getElementById("tablaCalificaciones");
    let datos=JSON.parse(localStorage.getItem("calificaciones"))||[];

    tabla.innerHTML="<tr><th>Nombre</th><th>Calificación</th><th>Acción</th></tr>";

    let suma=0;

    datos.forEach((c,i)=>{
        suma+=c.cal;

        tabla.innerHTML+=`
        <tr>
        <td>${c.nombre}</td>
        <td>${c.cal}</td>
        <td><button onclick="eliminarCal(${i})">Eliminar</button></td>
        </tr>`;
    });

    let promedio=datos.length? (suma/datos.length).toFixed(2):0;

    tabla.innerHTML+=`
    <tr>
    <td><b>PROMEDIO</b></td>
    <td colspan="2"><b>${promedio}</b></td>
    </tr>`;
}

// ELIMINAR CALIFICACIÓN
function eliminarCal(i){
    let datos=JSON.parse(localStorage.getItem("calificaciones"));
    datos.splice(i,1);
    localStorage.setItem("calificaciones",JSON.stringify(datos));
    cargarCalificaciones();
}

</script>

</body>
</html>
