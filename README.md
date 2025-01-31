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

**Consulta realizada:**
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

**Consulta realizada:**
```
insert into EmpresasFCT (nombre,quiereAlumnos,numAlumnos,fechaContacto) values ('Mango',true,2,'03/09/2025'),
('Movistar',true,3,'03/08/2025'),
('Fanny',false,0,'02/20/2025'),
('Safari',true,2,'03/12/2025'),
('Clear',true,1,'03/15/2025');
```

## Apartado 3
Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT
ordenados por fechaContacto, de modo que en la primera la salga el que tenga la
fecha más reciente.

**Consulta realizada**
```
select * from EmpresasFCT order by fechaContacto asc;
```

![image](https://github.com/user-attachments/assets/8c993820-1744-466c-b67e-d3429ab58fcb)

## Apartado 4
Realiza una consulta que permita obtener un listado de todos los contactos de
Odoo (no empresas) con la siguiente información:
- Nombre
- Cuya ciudad sea Tracy
- Nombre comercial de la empresa
Ordenados alfabéticamente por el nombre comercial de la empresa.

**Consulta realizada:**
```
select name,city,commercial_company_name from res_partner where company_id is null and city = 'Tracy' order by commercial_company_name asc;
```

![image](https://github.com/user-attachments/assets/16a4e7c9-745a-4f58-bb52-160561186254)


## Apartado 5
Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han
emitido algún reembolso (facturas recticativas de proveedor).
- Nombre de la empresa
- Número de factura
- Fecha de la factura
- Total factura SIN impuestos
Ordenadas por fecha de factura de modo que la primera sea la más reciente.

**Consulta realizada**
```
select 
c.name,
p.name,
p.invoice_date,
p.amount_untaxed_signed 
from res_partner c 
left join account_move p on p.partner_id=c.id
where p.move_type='in_refund' 
order by p.invoice_date desc;
```

## Apartado 6
Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les
ha emitido más de dos facturas de venta (solo venta) conrmadas, mostrando los
siguientes datos:
- Nombre de la empresa
- Número de facturas 
- Total facturado SIN IMPUESTOS

**Consulta realizada**
```

```
