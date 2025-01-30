# TAREA 12
## Apartado 1
Mediante la
herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una
sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos:

● idEmpresa: autonumérico. Este campo será la clave primaria.

● nombre: Texto con tamaño máximo de 40 caracteres. 

● quiereAlumnos: Booleano.

● numAlumnos: número entero.

● fechaContacto: tipo fecha

Consulta realizada:
````
create table EmpresasFCT(
  idEmpresa INT PRIMARY KEY,
  nombre VARCHAR(40),
  quiereAlumnos boolean,
  numAlumnos INT,
  fechaContacto DATE
);
````

![image](https://github.com/user-attachments/assets/57903728-4bab-4983-8ef7-e17673ccec52)
