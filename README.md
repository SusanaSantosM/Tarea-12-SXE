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
  idEmpresa SERIAL PRIMARY KEY,
  nombre VARCHAR(40),
  quiereAlumnos boolean,
  numAlumnos INT,
  fechaContacto DATE
);
````

![image](https://github.com/user-attachments/assets/89bd2e58-22cb-40da-9fb3-3b7dd5dae897)


## Apartado 2
Inserta 5 registros inventados en la tabla a través de una sentencia SQL.

Consulta realizada:
```
insert into EmpresasFCT (nombre,quiereAlumnos,numAlumnos,fechaContacto) values ('Mango',true,2,'03/09/2025'),
('Fanny',false,0,'02/20/2025'),
('Safari',true,2,'03/12/2025'),
('Movistar',true,3,'03/08/2025'),
('Clear',true,1,'03/15/2025');
```
