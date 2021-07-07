# ScritBDAlquilerVehiculos

CREACIÓN DE TABLAS

                                ALQUILER
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[alquiler]    Script Date: 06/07/2021 13:15:34 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[alquiler](
	[Id_alquiler] [int] IDENTITY(1,1) NOT NULL,
	[Id_vehiculo] [int] NOT NULL,
	[Id_cliente] [int] NOT NULL,
	[numero_dias] [int] NOT NULL,
	[estado_vehiculo] [varchar](max) NOT NULL,
	[ciudad_origen] [nchar](20) NOT NULL,
	[ciudad_destino] [nchar](20) NOT NULL,
	[galones_entregado] [decimal](18, 2) NOT NULL,
	[Id_factura] [int] NOT NULL,
	[calificacion] [nchar](10) NOT NULL,
	[fecha_entrega] [date] NOT NULL,
	[fecha_devuelta] [date] NOT NULL,
	[galones_recibidos] [decimal](18, 2) NOT NULL,
 CONSTRAINT [PK_alquiler] PRIMARY KEY CLUSTERED 
(
	[Id_alquiler] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]

GO

ALTER TABLE [dbo].[alquiler] ADD  CONSTRAINT [DF_alquiler_calificacion]  DEFAULT ('Excelente') FOR [calificacion]
GO

ALTER TABLE [dbo].[alquiler]  WITH CHECK ADD  CONSTRAINT [FK_alquiler_cliente] FOREIGN KEY([Id_cliente])
REFERENCES [dbo].[cliente] ([Id_cliente])
GO

ALTER TABLE [dbo].[alquiler] CHECK CONSTRAINT [FK_alquiler_cliente]
GO

ALTER TABLE [dbo].[alquiler]  WITH CHECK ADD  CONSTRAINT [FK_alquiler_factura] FOREIGN KEY([Id_factura])
REFERENCES [dbo].[factura] ([Id_factura])
GO

ALTER TABLE [dbo].[alquiler] CHECK CONSTRAINT [FK_alquiler_factura]
GO

                                    CLIENTE
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[cliente]    Script Date: 06/07/2021 13:17:43 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[cliente](
	[Id_cliente] [int] IDENTITY(1,1) NOT NULL,
	[nombres] [varchar](50) NOT NULL,
	[apellidos] [varchar](50) NOT NULL,
	[genero] [nchar](1) NOT NULL,
	[direccion_domiciliaria] [varchar](60) NOT NULL,
	[telefono_domicilio] [nchar](15) NOT NULL,
	[telefono_familiar] [nchar](15) NOT NULL,
	[tipo_sangre] [nchar](2) NOT NULL,
 CONSTRAINT [PK_clientes] PRIMARY KEY CLUSTERED 
(
	[Id_cliente] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

                                 COTIZACION_VEHICULO
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[cotizacion_vehiculo]    Script Date: 06/07/2021 13:18:31 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[cotizacion_vehiculo](
	[rango_inicial] [int] NOT NULL,
	[rango_final] [int] NOT NULL,
	[Id_cotizacion] [int] IDENTITY(1,1) NOT NULL,
	[Id_vehiculo] [int] NOT NULL,
	[valor] [decimal](18, 2) NOT NULL,
 CONSTRAINT [PK_cotizacion_vehiculo] PRIMARY KEY CLUSTERED 
(
	[Id_cotizacion] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[cotizacion_vehiculo]  WITH CHECK ADD  CONSTRAINT [FK_cotizacion_vehiculo_vehiculo] FOREIGN KEY([Id_vehiculo])
REFERENCES [dbo].[vehiculo] ([Id_vehiculo])
GO

ALTER TABLE [dbo].[cotizacion_vehiculo] CHECK CONSTRAINT [FK_cotizacion_vehiculo_vehiculo]
GO
           
                                   EMPLEADO
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[empleado]    Script Date: 06/07/2021 13:20:08 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[empleado](
	[cargo] [nchar](25) NOT NULL,
	[Id_empleado] [int] IDENTITY(1,1) NOT NULL,
	[nombres] [varchar](50) NOT NULL,
	[apellidos] [varchar](50) NOT NULL,
	[genero] [nchar](1) NOT NULL,
	[direccion_domiciliaria] [varchar](60) NOT NULL,
	[telefono_domicilio] [nchar](15) NOT NULL,
	[telefono_familiar] [nchar](15) NOT NULL,
	[tipo_sangre] [nchar](2) NOT NULL,
 CONSTRAINT [PK_empleado] PRIMARY KEY CLUSTERED 
(
	[Id_empleado] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

                                    ESTACIONAMIENTO

USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[estacionamiento]    Script Date: 06/07/2021 13:21:34 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[estacionamiento](
	[ubicacion] [varchar](70) NOT NULL,
	[estado] [nchar](1) NOT NULL,
	[codigo] [nchar](6) NOT NULL,
	[Id_estacionamiento] [int] IDENTITY(1,1) NOT NULL,
 CONSTRAINT [PK_estacionamiento] PRIMARY KEY CLUSTERED 
(
	[Id_estacionamiento] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

                                     FACTURA
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[factura]    Script Date: 06/07/2021 15:25:04 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[factura](
	[Id_factura] [int] IDENTITY(1,1) NOT NULL,
	[total] [decimal](18, 2) NOT NULL,
	[fecha_emision] [datetime] NOT NULL,
	[iva] [decimal](18, 2) NOT NULL,
	[descuento] [decimal](18, 2) NOT NULL,
 CONSTRAINT [PK_factura] PRIMARY KEY CLUSTERED 
(
	[Id_factura] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

                                   FACTURA_DETALLE
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[factura_detalle]    Script Date: 06/07/2021 13:22:10 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[factura_detalle](
	[Id_factura_detalle] [int] IDENTITY(1,1) NOT NULL,
	[Id_factura] [int] NOT NULL,
	[Id_producto] [int] NOT NULL,
	[descripcion] [varchar](60) NOT NULL,
	[valor_unitario] [decimal](18, 2) NOT NULL,
	[unidad] [int] NOT NULL,
	[valor_total] [decimal](18, 2) NOT NULL,
 CONSTRAINT [PK_factura_detalle] PRIMARY KEY CLUSTERED 
(
	[Id_factura_detalle] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[factura_detalle]  WITH CHECK ADD  CONSTRAINT [FK_factura_detalle_productos] FOREIGN KEY([Id_producto])
REFERENCES [dbo].[producto] ([Id_producto])
GO

ALTER TABLE [dbo].[factura_detalle] CHECK CONSTRAINT [FK_factura_detalle_productos]
GO

                                  MANTENIMIENTO
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[factura_detalle]    Script Date: 06/07/2021 13:22:10 ******/
SET ANSI_NULLS ON



USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[mantenimiento]    Script Date: 06/07/2021 13:22:46 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[mantenimiento](
	[fecha_inicio] [datetime] NOT NULL,
	[fecha_fin] [datetime] NOT NULL,
	[Id_matenimiento] [int] IDENTITY(1,1) NOT NULL,
	[Id_factura] [int] NOT NULL,
	[Id_empleado] [int] NOT NULL,
	[valor] [decimal](18, 2) NOT NULL,
	[descripcion] [varchar](80) NOT NULL,
	[Id_vehiculo] [int] NOT NULL,
 CONSTRAINT [PK_mantenimiento] PRIMARY KEY CLUSTERED 
(
	[Id_matenimiento] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[mantenimiento]  WITH CHECK ADD  CONSTRAINT [FK_mantenimiento_empleado] FOREIGN KEY([Id_empleado])
REFERENCES [dbo].[empleado] ([Id_empleado])
GO

ALTER TABLE [dbo].[mantenimiento] CHECK CONSTRAINT [FK_mantenimiento_empleado]
GO

ALTER TABLE [dbo].[mantenimiento]  WITH CHECK ADD  CONSTRAINT [FK_mantenimiento_vehiculo] FOREIGN KEY([Id_vehiculo])
REFERENCES [dbo].[vehiculo] ([Id_vehiculo])
GO

ALTER TABLE [dbo].[mantenimiento] CHECK CONSTRAINT [FK_mantenimiento_vehiculo]
GO

                                 PRODUCTO
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[producto]    Script Date: 06/07/2021 13:23:33 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[producto](
	[Id_producto] [int] IDENTITY(1,1) NOT NULL,
	[descripcion] [varchar](150) NULL,
	[unidad] [int] NULL,
	[valor] [decimal](18, 2) NULL,
	[editable] [bit] NULL,
 CONSTRAINT [PK_productos] PRIMARY KEY CLUSTERED 
(
	[Id_producto] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

                                 VEHICULO
USE [alquilervehiculos]
GO

/****** Object:  Table [dbo].[vehiculo]    Script Date: 06/07/2021 13:24:11 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[vehiculo](
	[placa] [varchar](10) NOT NULL,
	[modelo] [nchar](10) NOT NULL,
	[color] [nchar](10) NOT NULL,
	[marca] [nchar](10) NOT NULL,
	[año] [nchar](10) NOT NULL,
	[fecha_fabricacion] [date] NOT NULL,
	[Id_vehiculo] [int] IDENTITY(1,1) NOT NULL,
	[Id_estacionamiento] [int] NOT NULL,
 CONSTRAINT [PK_vehiculo] PRIMARY KEY CLUSTERED 
(
	[Id_vehiculo] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[vehiculo]  WITH CHECK ADD  CONSTRAINT [FK_vehiculo_estacionamiento] FOREIGN KEY([Id_estacionamiento])
REFERENCES [dbo].[estacionamiento] ([Id_estacionamiento])
GO

ALTER TABLE [dbo].[vehiculo] CHECK CONSTRAINT [FK_vehiculo_estacionamiento]
GO


                                 INSERCIÓN DE DATOS

                       ALQUILER
INSERT INTO [dbo].[alquiler]([Id_vehiculo],[Id_cliente],[numero_dias],[estado_vehiculo],
[ciudad_origen],[ciudad_destino],[galones_entregado],[Id_factura],[calificacion],
[fecha_entrega],[fecha_devuelta],[galones_recibidos])
VALUES(1,1, 1,'se entrego todo completo','Manta','Rocafuerte',5.2,1,'buena','25-06-2020','26-06-2020',3.5);
(10,1, 2,'se entrego carro con leve choque en la parte trasera','Manta','Calceta',4.2,2,'regular','12-05-2021','14-05-2021',4.1);
(11,4, 1,'se entrego coche en perfectas condiciones','Manta','Portoviejo',6.2,3,'excelente','23-10-2020','24-10-2020',6.2);
(14,6, 1,'se entrego coche con mucho lodo','Manta','Jaramijo',5,4,'regular','29-06-2021','30-06-2021',4);
(13,7, 2,'llantas desinfladas','Portoviejo','Manta',4,5,'buena','09-03-2021','11-03-2021',3.6);
(15,3,1,'con un retrovisor raspado','Portoviejo','Pajan',6.6,7,'regular','01-07-2021','02-07-2021',4);
(17,5,1,'una luz partida','Portoviejo','Sucre',8,8,'mala','05-05-202|','06-05-2021',7.3);

                       CLIENTE
INSERT INTO [dbo].[cliente]([nombres],[apellidos],[genero],[direccion_domiciliaria],
[telefono_domicilio],[telefono_familiar],[tipo_sangre])
VALUES('fabricio','ortiz','m','calle 116 y av 203','052920521','0992580602','O+');
VALUES('carlos','moreira','m','barrio altamira','052920544','0982580609','O+');
VALUES('manuel','quiroz','m','barrio los esteros','052840521','0982780592','B+');
VALUES('paul','delgado','m','barrio la aurora','053527712','0999885606','B-');
VALUES('ana','perlaza','f','maria auxiliadora','052922691','0998880608','O+');
VALUES('ignacio','contreras','m','ciudadela universitaria','052966721','0982982604','O+');
VALUES('juan','alava','m','calle 203 av 18','052929555','0985225520','O+');

                     COTIZACION_VEHICULO
INSERT INTO [dbo].[cotizacion_vehiculo]([rango_inicial],
[rango_final],[Id_vehiculo],[valor])
VALUES(1,4,1,50.30);(2,3,10,40.6);(1,3,12,30);(2,3,11,40.18);
(1,5,13,60.38);(1,4,16,69.23);(2,5,15,59.67);

                      EMPLEADO
INSERT INTO [dbo].[empleado]([cargo],[nombres],[apellidos],[genero],
[direccion_domiciliaria],[telefono_domicilio],[telefono_familiar],[tipo_sangre])
VALUES('limpiador','eduardo','medranda','m','barrio las brisas','052920661','0982880805','O+');
VALUES('mecanico','lenin','moreira','m','barrio umiña','052989786','0992345666','B+');
VALUES('mecanico','jacinto','espinoza','m','barrio altagracia','052729681','0982880805','O+');
VALUES('mecanico','diana','mendoza','f','barrio la aurora','052926941','0992881166','B-');
VALUES('limpiador','emanuel','roca','m','barrio la proaño','052920544','0999983496','B-');
VALUES('mecanico','dario','paredes','m','barrio la dolorosa','052628779','0993986798','O+');

                           ESTACIONAMIENTO
INSERT INTO [dbo].[estacionamiento]
([ubicacion],[estado],[codigo])
VALUES('diagonal al norte','A','MUR7D9');
('en el centro de la ciudad','A','ZAF4D5');
('diagonal al shopping','A','GNE94U');
('calle 13 local tu estacionamiento','A','PTHD84');
('Atras hielo polar','A','VYJ6U7');
('A 2 cuadras del seguro social','A','QGJ7H0');

                        FACTURA
INSERT INTO [dbo].[factura]([total]
,[fecha_emision],[iva],[descuento])
VALUES(45.50,'25/06/2021',6.36,15);(50.60,'22/05/2020',5,10);
(49.10,'15/04/2020',5,8);(30.20,'21/07/2020',10,5);
(50,'29/05/2020',9,10);(25.35,'15/06/2021',5,10);
(57.28,'18/08/2020',5,10);(80.48, '28/11/2020', 2,5);

                        FACTURA_DETALLE
INSERT INTO [dbo].[factura_detalle]([Id_factura],[Id_producto],
[descripcion],[valor_unitario],[unidad],[valor_total])
VALUES(2,1,'se cancelo el alquiler',50,2,80.30);
(9,1,'se cancelo el alquiler',60,1,90.67);
(6,1,'se cancelo el alquiler y los daños',50,2,250);

                      MANTENIMIENTO
INSERT INTO [dbo].[mantenimiento]([fecha_inicio],
[fecha_fin],[Id_factura],[Id_empleado],[valor],[descripcion],[Id_vehiculo])
VALUES('15/02/2020','16/02/2020',1, 1,35.40,'limpieza de filtros gasolina y cambio de aceite', 1);
('13/01/2020','17/01/2020',2, 2, 1000.50,'Bajada de maquina', 10);
('27/01/2021','28/01/2020',3, 3, 1000.50,'Lavado de maquina', 12);
('17/02/2021','17/02/2020',4, 4, 1000.50,'Cambio de filtros de gasolina', 14);
('05/03/2019','06/03/2019',5, 5, 80.50,'Cambio de amortiguadores delanteros', 15);
('16/04/2021','18/04/2020',7, 1, 170,'Cambio de amortiguadores delanteros y traseros', 1);

                        PRODUCTO
INSERT INTO [dbo].[productos]([descripcion]
,[unidad],[valor],[editable])
VALUES ('aceite de motor', 1, 20.15,1);
VALUES ('filtro', 1, 2.00,1);
VALUES ('neumáticos', 1, 80.35,1);
VALUES ('luces', 1, 30,1);
VALUES ('liquido de freno', 1, 20.15,1);
VALUES ('aceite hidraulico', 1, 24.10,1);
VALUES ('bateria', 1, 150.58,1);
VALUES ('amortiguadores', 1, 250.25,1);

                         VEHICULO
INSERT INTO [dbo].[vehiculo]([placa],[modelo],
[color],[marca],[año],[fecha_fabricacion],[Id_estacionamiento])
VALUES ('IBK089', 'Aveo', 'rojo', 'Chevrolet', '2008', '05/06/2007', 1);
VALUES ('HKK897', 'Soluto', 'negro', 'Kia', '2020', '05/12/2019', 2);
VALUES ('MHT858', 'Ecosport', 'negro', 'Ford', '2006', '05/07/2005', 3);
VALUES ('MMG759', 'Corsa', 'azul', 'Chevrolet', '2007', '05/01/2007', 5);
VALUES ('KMH677', 'Hilux', 'azul', 'Toyota', '2012', '05/09/2011', 4);
VALUES ('LOL990', 'Versa', 'amarillo', 'Nissan', '2012', '05/10/2011', 6);
VALUES ('MSS447', 'Sportage', 'amarillo', 'Kia', '2021', '05/11/2020', 7);
VALUES ('GYM761', 'Picanto', 'amarillo', 'Kia', '2021', '29/11/2020', 7);


                                 CONSULTAS
1) Por cada año el total de facturas que se han otorgado y la cantidad de dinero que ha ingresado.  Si yo quiero que en el año 2021 se han 
omitido 100 facturas y he obtenido el total de ingreso de 20.000 dólares. En el año 2022 he omitido 99 facturas y he obtenido un ingreso de 
30.000 dólares, y asi por cada año.

select year (fecha_emision) as año, sum(total) as total, count(*) as numero_factura
from factura group by year(fecha_emision);


2) Quiero que me salga el nombre de los clientes y cuantas veces ha alquilado vehiculos ese cliente. Por ejemplo, yo he alquilado 20 veces 
vehiculos.

select c.Id_cliente, CONCAT (c.nombres,' ',c.apellidos) as Clientes, count(*) as Veces_Alquilado
from alquiler  a inner join cliente c on a.Id_cliente = c.Id_cliente
group by c.Id_cliente, CONCAT (c.nombres,' ',c.apellidos);



3) Quiero que me salga todos los vehiculos de la institución y cuantas veces han estado en mantenimiento.

select count(Id_matenimiento) as veces_mantenimiento,  placa, modelo from mantenimiento m 
right join vehiculo v on m.Id_vehiculo = v.Id_vehiculo
group by placa, modelo;

4) Quiero que me salgan todos los vehiculos y cuantos años llevan en la institución. Es decir, el vehiculo IBCKK001 lleva 10 años 
en la institución, en años, meses, días o como yo quiera ponerle y ordenado ascendentemente, y es bueno porque asi veo que vehiculo 
es más antiguo para hacerle un reemplazo.


select DATEDIFF(YEAR,fecha_fabricacion, GETDATE()) 
as años, placa, modelo from vehiculo 
order by años asc;

