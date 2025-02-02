# TAREA 12
## Apartado 1
>Mediante la herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una
>sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos:
>
>● idEmpresa: autonumérico. Este campo será la clave primaria.
>
>● nombre: Texto con tamaño máximo de 40 caracteres. 
>
>● quiereAlumnos: Booleano.
>
>● numAlumnos: número entero.
>
>● fechaContacto: tipo fecha

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
>Inserta 5 registros inventados en la tabla a través de una sentencia SQL.

**Consulta realizada:**
```
insert into EmpresasFCT (nombre,quiereAlumnos,numAlumnos,fechaContacto) values ('Mango',true,2,'03/09/2025'),
('Movistar',true,3,'03/08/2025'),
('Fanny',false,0,'02/20/2025'),
('Safari',true,2,'03/12/2025'),
('Clear',true,1,'03/15/2025');
```

## Apartado 3
>Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT
>ordenados por fechaContacto, de modo que en la primera la salga el que tenga la
>fecha más reciente.

**Consulta realizada**
```
select * from EmpresasFCT order by fechaContacto asc;
```

![image](https://github.com/user-attachments/assets/8c993820-1744-466c-b67e-d3429ab58fcb)

## Apartado 4
>Realiza una consulta que permita obtener un listado de todos los contactos de
>Odoo (no empresas) con la siguiente información:
>- Nombre
>- Cuya ciudad sea Tracy
>- Nombre comercial de la empresa
>Ordenados alfabéticamente por el nombre comercial de la empresa.

**Consulta realizada:**
```
select name,city,commercial_company_name from res_partner where is_company=false and city = 'Tracy' order by commercial_company_name asc;
```

![image](https://github.com/user-attachments/assets/8d3cfbe1-7045-4c29-82eb-cc4db72374b2)


## Apartado 5
>Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han
>emitido algún reembolso (facturas recticativas de proveedor).
>- Nombre de la empresa
>- Número de factura
>- Fecha de la factura
>- Total factura SIN impuestos
>Ordenadas por fecha de factura de modo que la primera sea la más reciente.

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
>Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les
>ha emitido más de dos facturas de venta (solo venta) conrmadas, mostrando los
>siguientes datos:
>- Nombre de la empresa
>- Número de facturas 
>- Total facturado SIN IMPUESTOS

**Consulta realizada**
```
select 
	invoice_partner_display_name as Nombre_empresa,
	count(distinct name) as numero_facturas,
	sum(distinct amount_untaxed) as total_facturado_sin_impuestos
from account_move 
where move_type='out_invoice'
group by invoice_partner_display_name
having count(distinct name) > 2;
```

## Apartado 7
>Crea una sentencia que actualice el correo de los contactos cuyo dominio es @bilbao.example.com a >@bilbao.bizkaia.neus

**Consulta realizada:**
```
update res_partner set email = 'info@bilbao.bizkaia.neus' where email = 'info@bilbao.example.com';
```
<details>
 <summary>Saldra un aviso de actualización de datos</summary>
<br>
  
![image](https://github.com/user-attachments/assets/1a1a6686-3997-4282-8c3f-a6699a223b8a)

</details>

Verificamos si el cambio fue correcto.

![image](https://github.com/user-attachments/assets/1ec0bafd-c76a-4bab-bb7b-1b2aca31a675)


## Apartado 8
>La empresa Ready Mat ha hecho un ERE y ha despedido a todos los empleados que tenías como contacto. Crea >una sentencia que elimine todos los contactos pertenecientes a la empresa “Ready Mat”, pero mantén la >empresa. Añade una captura de pantalla de la sección de contactos de odoo con Ready Mat antes y después.

Primero vamos hacer una captura de los contactos que tenemos en Odoo entre ellos de la empresa "Ready Mat".

 ![image](https://github.com/user-attachments/assets/2c6b3913-e4cf-4216-8888-33bbe3b56605)

Una de las maneras de asegurarnos cuales son los contactos de la empresa "Ready Mat" es en Odoo, especificando en la busquedad el nombre de la empresa y apareceran los empleados ligados a esta empresa. Otra forma es en la misma base de datos. Veamoslo de ambas maneras:

<details>
  <summary>Contactos de Ready Mat en Odoo</summary>
	
![image](https://github.com/user-attachments/assets/9da81995-f396-487c-823f-b6c2530b5387)

</details>

<details>
  <summary>Contactos de Ready Mat en la base de datos PgAdmin</summary>
  <br> Consulta: 
	
  ```
select * from res_partner 
where commercial_company_name='Ready Mat' and is_company=false;
  ```
	
![image](https://github.com/user-attachments/assets/3d265ded-afb2-4332-af44-2b54490365fa)

</details>

Ahora borraremos los contactos de la empresa "Ready Mat" manteniendo el contacto de la empresa. Utilizamos la siguiente consulta:

```
delete from res_partner 
where commercial_company_name='Ready Mat' and is_company=false;
```

Confirmamos en los contactos de Odoo

![image](https://github.com/user-attachments/assets/55effbae-dbc7-4022-8df4-d3ccb943dda3)
