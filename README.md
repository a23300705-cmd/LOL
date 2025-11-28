# 🎮 PESCADOS — Proyecto Integrador  
**Autor:** Chavarría Montes Eduardo Miguel  
**Carrera:** Desarrollo de Software  
**Fecha:** 2025  

---

# 📘 Descripción General
PESCADOS es un videojuego desarrollado en **C# con Windows Forms** que implementa toda la lógica del juego directamente en una **base de datos MySQL**, cumpliendo con los requisitos del Proyecto Integrador.

Además, se utiliza **MongoDB (Cluster en la nube)** para almacenar información no estructurada como logs de eventos del jugador, historial y otros datos complementarios.

El proyecto sigue la regla fundamental:

> ⚠️ **C# NO ejecuta SQL directo.**  
> Toda inserción, actualización, eliminación o consulta a tablas se hace mediante:  
> ✔ Stored Procedures  
> ✔ Vistas sanitizadas  

---

# 📂 Contenido del Proyecto

PESCADOS/
│── Proyecto_C#/ ← Código completo C# + solución .sln
│── Ejecutable/ ← Carpeta Release con el .exe
│── SQL/
│ ├── pescados.sql ← Dump completo (estructura + SP + vistas + datos)
│ ├── estructura.sql ← (Opcional) Tablas
│ ├── procedures.sql ← (Opcional) Procedimientos almacenados
│ └── vistas.sql ← (Opcional) Vistas sanitizadas
│── Mongo/
│ ├── instrucciones_mongo.md ← Conexión al cluster
│ └── ejemplo_documentos.json ← (Opcional) Ejemplos de logs/eventos
│── README.md ← Este archivo
│── README.txt ← Versión plana del README
│── Assets/ ← Imágenes, recursos del juego

markdown
Copiar código

---

# ⚙️ Tecnologías Utilizadas

| Tecnología | Uso |
|-----------|-----|
| **C# Windows Forms** | Interfaz gráfica, navegación, interacción |
| **MySQL** | Base de datos principal — lógica del juego |
| **Stored Procedures** | Toda la lógica: XP, oro, partidas, logros, métricas |
| **Vistas Sanitizadas** | Consultas permitidas desde C# |
| **MongoDB (Cluster)** | Logs, historial, datos no estructurados |
| **.NET Framework** | Ejecución del proyecto |

---

# 🗄️ Base de Datos MySQL  
Toda la lógica del juego está implementada en MySQL mediante:

## 📌 Tablas principales:
- jugadores  
- partidas  
- capturas  
- logros  
- jugador_logro  
- items/pesca/tienda (según tu proyecto)

## 📌 Stored Procedures importantes:
- `sp_LoginUsuario`  
- `sp_IniciarPartida`  
- `sp_FinalizarPartida`  
- `sp_RegistrarCaptura`  
- `sp_VerificarLogros`  
- `sp_ReclamarLogro`  
- `sp_ActualizarOroXP`  
- `sp_InsertarPartida`  
- `sp_GetEstadisticasJugador`  

## 📌 Vistas Sanitizadas:
- `v_jugador_datos`
- `v_logros_completados`
- `v_logros_pendientes`
- `v_estadisticas_partidas`

✔ C# **solo** puede hacer `SELECT` a estas vistas.

---

# 💾 Restauración de la Base de Datos (MySQL)

## 1. Crear la base:
```sql
CREATE DATABASE pescados CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
2. Importar dump completo:
bash
Copiar código
mysql -u root -p pescados < SQL/pescados.sql
Después de esto quedan:
✔ Tablas
✔ SP
✔ Vistas
✔ Datos de prueba

🍃 MongoDB (Cluster en la nube)
El proyecto utiliza MongoDB Atlas para almacenar:

Logs del jugador

Eventos del juego

Datos no estructurados

El string de conexión está documentado en:

bash
Copiar código
Mongo/instrucciones_mongo.md
Ejemplo genérico:

txt
Copiar código
mongodb+srv://usuario:password@cluster.mongodb.net/pescados_logs
Colecciones utilizadas:

logs_eventos

acciones_jugador

tienda_rotaciones

Ejemplos en:

bash
Copiar código
Mongo/ejemplo_documentos.json
📊 Sistema de Métricas (Requisito obligatorio)
El juego registra métricas como:

Oro total ganado

XP total ganada

Número de capturas

Partidas jugadas

Tiempo de juego

Logros desbloqueados

Estas métricas se consultan mediante:

sp_GetEstadisticasJugador

v_estadisticas_partidas

Y se muestran con gráficas en Windows Forms.

🏆 Sistema de Logros (Achievements)
Cada logro tiene:

Nombre

Descripción

Condición

Estado (pendiente / completado)

Toda la lógica se maneja en la BD con SP:

sp_VerificarLogros

sp_ReclamarLogro

sp_OtorgarLogro

Interfaz en Windows Forms:

Logros completados (con recompensa reclamada)

Logros pendientes

▶️ Cómo Ejecutar el Juego
Tener MySQL ejecutándose.

Tener internet (MongoDB cluster requiere conexión).

Restaurar pescados.sql.

Abrir:

Copiar código
Ejecutable/PESCADOS.exe
Iniciar sesión con usuario de prueba:

makefile
Copiar código
Usuario: demo
Contraseña: demo123
✔ Cumplimiento de Requisitos (Checklist oficial)
Requisito	Estado
C# Windows Forms	✔ Cumplido
Base de datos SQL	✔ MySQL
Toda la lógica en BD	✔ Toda la lógica en SP
Sin SQL directo en C#	✔ Totalmente prohibido y cumplido
Vistas sanitizadas	✔ Implementadas
MongoDB obligatorio	✔ Cluster funcionando
Métricas del juego	✔ Implementadas y visibles
Sistema de logros	✔ Completamente funcional
Entregable completo	✔

📧 Datos del Autor
Nombre: Chavarría Montes Eduardo Miguel
Carrera: Desarrollo de Software
Correo: (agregar tu correo)

📝 Notas Finales
El proyecto fue desarrollado siguiendo todas las restricciones y normas del Proyecto Integrador.

El archivo pescados.sql permite reconstruir la BD completa.

MongoDB funciona remotamente mediante un cluster para evitar pérdida de datos.

El código C# está completamente aislado de SQL directo.
