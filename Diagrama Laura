create table ejercicio.rol(
    name varchar(50)not null,
    constraint pk_rol primary key (name)
);
create table ejercicio.user(
	login varchar(50)not null,
	password varchar(60)not null,
	email varchar(254)unique not null,
	activated int not null,
	lang_key varchar(6)not null,	
	image_ur varchar(256)null,
	activation_key varchar(20)null,
	reset_key varchar(20)null,
	reset_date timestamp null,
	constraint PK_login primary key (login),
	constraint uc_email unique (email)
);
create table ejercicio.user_authority(
    name_rol varchar(50)not null,
    login varchar(50)not null,
    constraint pk_user_authority primary key (name_rol,login),
    constraint fk_rol foreign key (name_rol)references ejercicio.rol(name)
     on update cascade on delete restrict,	
    constraint fk_user foreign key (login)references ejercicio.user(login)
     on update cascade on delete restrict
);

create table ejercicio.cliente(
	numero_documento varchar(50)not null,
	primer_nombre varchar(50)not null,
	segundo_nombre varchar(50)null,
	primer_apellido varchar(50)not null,
	segundo_apellido varchar(50)null,
	sigla varchar(10)not null,
	login varchar(50)not null,
	constraint pk_cliente primary key (sigla,numero_documento),
	constraint FK_user foreign key (login)references ejercicio.user(login)
	on update cascade on delete restrict,
	constraint uc_login unique (login)
);
create table ejercicio.tipo_documento(
	sigla varchar(10)not null,
	nombre_documento varchar(100)not null,
	estado varchar(40),
	constraint PK_sigla primary key(sigla),
	constraint UC_nombre_documento unique (nombre_documento)
);
 create table ejercicio.log_auditoria(
    id int4 not null,
    nivel varchar (400)not null,
    log_name varchar(400)not null,
    mensaje varchar (400)not null,
    fecha date not null,
    numero_documento varchar(50)not null,
    sigla varchar(10)not null,
    constraint pk_log_auditoria primary key (id),
    constraint fk_cliente foreign key (numero_documento,sigla)references ejercicio.cliente(numero_documento,sigla)
     on update cascade on delete restrict 
);
 create table ejercicio.log_errores(
    id int4 not null,
    nivel varchar(400) not null,
    log_name varchar(400)not null,
    mensaje varchar (400)not null,
    fecha date not null,
    numero_documento varchar(50)not null,
    sigla varchar(10)not null,
    constraint pk_log_errores primary key (id),
    constraint fk_cliente foreign key (numero_documento,sigla)references ejercicio.cliente(numero_documento,sigla)
     on update cascade on delete restrict 
);
--Package sede
 create table ejercicio.tipo_ambiente(
    tipo varchar(50) not null,
    descripcion varchar(100) not null,
    estado varchar(40) not null,
    constraint pk_tipo_ambiente primary key (tipo)
);
  create table ejercicio.sede(
    nombre_sede varchar(50) not null,
    direccion varchar(400) not null,
    estado varchar(40) not null,
    constraint pk_sede primary key (nombre_sede)
);
 create table ejercicio.ambiente(
    numero_ambiente varchar(50) not null,
    nombre_sede varchar(50) not null,
    descripcion varchar(1000) not null,
    estado varchar(40) not null,
    limitacion varchar(40) not null,
    tipo varchar(50) not null,
    constraint pk_ambiente primary key (numero_ambiente,nombre_sede),
    constraint fk_sede foreign key (nombre_sede)references ejercicio.sede (nombre_sede)
     on update cascade on delete restrict ,
    constraint fk_tipo_ambiente foreign key (tipo)references ejercicio.tipo_ambiente (tipo)
     on update cascade on delete restrict 
 );

 create table ejercicio.limitacion_ambiente(
    numero_ambiente varchar(50) not null,
    nombre_sede varchar(50) not null,
    codigo_resultado varchar(40) not null,
    codigo_competencia varchar(50) not null,
    codigo_programa varchar(50) not null,
    version_programa varchar(40) not null,
    constraint pk_limitacion_ambiente primary key (numero_ambiente,nombre_sede,codigo_resultado,codigo_competencia,codigo_programa,version_programa),
    constraint fk_ambiente foreign key (numero_ambiente,nombre_sede)references ejercicio.ambiente (numero_ambiente,nombre_sede)
    on update cascade on delete restrict,
    constraint fk_resultado_aprendizaje foreign key (codigo_resultado,codigo_competencia,codigo_programa,version_programa)references ejercicio.resultado_aprendizaje (codigo_resultado,codigo_competencia,codigo_programa,version_programa)
    on update cascade on delete restrict 
 );
--Package ficha
create table ejercicio.estado_ficha(
    nombre_estado varchar (20) not null,
    estado int2 not null,
    constraint pk_estado_ficha primary key (nombre_estado)
);
create table ejercicio.jornada (
    sigla_jornada varchar (20) not null,
    nombre_jornada varchar (40) unique not null,
    descripcion varchar (100) not null,
    imagen_url varchar (1000) null,
    estado varchar (40) not null,
    constraint pk_sigla_jornada primary key (sigla_jornada),
    constraint nombre_jornada unique (nombre_jornada)
);
 create table ejercicio.programa(
	codigo varchar (50) not null,
	version varchar (40) not null,
	nombre varchar (500) not null,
	sigla varchar (40) not null,
	estado varchar (40) not null,
	nivel varchar (40) not null,
	constraint pk_programa primary key (codigo, version),
	constraint FK_nivel_formacion foreign key (nivel) references ejercicio.nivel_formacion (nivel)
	 on update cascade on delete restrict
);
create table ejercicio.ficha (
    numero_ficha varchar (100) not null,
	fecha_inicio date not null,
	fecha_fin date not  null,
	ruta varchar (40) not null,
	codigo varchar (50) not null,
	version varchar (40) not null,
	nombre_estado varchar (20) not null,
	sigla_jornada varchar (20) not null,
	constraint pk_ficha primary key (numero_ficha),
	constraint fk_programa foreign key (codigo, version) references ejercicio.programa (codigo, version),
	constraint fk_estado_ficha foreign key (nombre_estado) references ejercicio.estado_ficha (nombre_estado),
	constraint fk_jornada foreign key (sigla_jornada) references ejercicio.jornada (sigla_jornada)
);
create table ejercicio.trimestre (
    nombre_trimestre int4 not null,
	nivel varchar (40) not null,
	sigla_jornada varchar (20) not null,
	estado varchar (40) not null,
	constraint pk_nombre_trimestre primary key (nombre_trimestre,nivel,sigla_jornada),  
	constraint fk_nivel_formacion foreign key (nivel) references ejercicio.nivel_formacion(nivel),  
constraint fk_jornada foreign key (sigla_jornada) references ejercicio.jornada(sigla_jornada)   
);
--Package proyectos
create table ejercicio.proyecto(
	codigo varchar (50) not null,
	nombre varchar (500) not null,
	estado varchar (40) not null,
	codigo_programa varchar(50) not null,
	version varchar (40) not null,
	constraint pk_proyecto primary key (codigo),
	constraint fk_programa foreign key (codigo_programa,version)references ejercicio.programa (codigo,version)
     on update cascade on delete restrict
);
create table ejercicio.fase(
	nombre varchar (40) not null,
	estado varchar (40) not null,
	codigo_proyecto varchar(40) not null,
	constraint pk_fase primary key (nombre,codigo_proyecto),
	constraint FK_proyecto foreign key (codigo_proyecto) references ejercicio.proyecto(codigo)
	on update cascade on delete restrict
);
create table ejercicio.actividad_proyecto(
	numero_actividad int4 not null,
	descripcion_actividad varchar (400) not null,
	estado varchar (40) not null,
	nombre_fase varchar(40) not null,
	codigo_proyecto varchar(40) not null,
	constraint pk_actividad_proyecto primary key (numero_actividad,nombre_fase,codigo_proyecto),
	constraint FK_fase foreign key (nombre_fase,codigo_proyecto) references ejercicio.fase (nombre,codigo_proyecto)
);
--package Ficha
create table ejercicio.estado_formacion(
	nombre_estado varchar(40) not null ,
	estado varchar(40) not null,
	constraint pk_estado_formacion primary key (nombre_estado)
);
create table ejercicio.aprendiz(
	numero_documento varchar(50) not null ,
	sigla varchar(10) not null ,
	numero_ficha varchar(100) not null ,
	nombre_estado varchar(40)not null,
	constraint pk_aprendiz primary key (numero_documento,sigla,numero_ficha),
	constraint FK_cliente foreign key (numero_documento,sigla)references ejercicio.cliente (numero_documento,sigla),
	constraint FK_ficha foreign key (numero_ficha)references ejercicio.ficha (numero_ficha) on update cascade on delete restrict,
	constraint FK_estado_formacion foreign key (nombre_estado)references ejercicio.estado_formacion (nombre_estado) on update cascade on delete restrict
);
create table ejercicio.ficha_Planeacion(
	numero_ficha varchar(100)not null,
	codigo_planeacion varchar(40)not null,
	estado varchar(40) not null,
	constraint pk_ficha_Planeacion primary key (numero_ficha,codigo_planeacion),
	constraint FK_ficha foreign key (numero_ficha)references ejercicio.ficha (numero_ficha) on update cascade on delete restrict,
	constraint FK_Planeacion foreign key (codigo_planeacion)references ejercicio.Planeacion (codigo) on update cascade on delete restrict
);
Create table ejercicio.ficha_has_trimestre(
	numero_ficha varchar (100) not null,
	sigla_jornada varchar (20) not null,
	nivel varchar (40) not null,
	nombre_trimestre int4 not null,
	constraint pk_ficha_has_trimestre primary key (numero_ficha, sigla_jornada, nivel, nombre_trimestre),
	constraint FK_ficha foreign key (numero_ficha) references ejercicio.ficha (numero_ficha) on update cascade on delete restrict,
	constraint FK_trimestre foreign key (sigla_jornada, nivel,nombre_trimestre)references ejercicio.trimestre (sigla_jornada, nivel,nombre_trimestre) on update cascade on delete restrict
);
create table ejercicio.resultados_vistos(
	codigo_resultado varchar(40) not null,
	codigo_competencia varchar (50) not null,
	codigo_programa varchar(50) not null,
	version_programa varchar (40) not null,
	numero_ficha varchar (100)not null,
	sigla_jornada varchar (20) not null,
	nivel varchar (40) not null,
	nombre_trimestre int4 not null,
	codigo_planeacion varchar (40) not null,
	constraint pk_resultados_vistos primary key (codigo_resultado, codigo_competencia, codigo_programa,version_programa,numero_ficha,sigla_jornada,nivel,nombre_trimestre,codigo_planeacion),
	constraint FK_ficha_has_trimestre foreign key (numero_ficha,sigla_jornada,nivel,nombre_trimestre) references ejercicio.ficha_has_trimestre (numero_ficha,sigla_jornada,nivel,nombre_trimestre) on update cascade on delete restrict,
	constraint FK_Planeacion foreign key (codigo_planificacion) references ejercicio.Planeacion (codigo) on update cascade on delete restrict,
	constraint FK_resultado_aprendizaje foreign key (codigo_resultado, codigo_competencia, codigo_programa, version_programa) references ejercicio.resultado_aprendizaje (codigo_resultado, codigo_competencia, codigo_programa, version_programa) on update cascade on delete restrict
	);
--Package programado
create table ejercicio.nivel_formacion(
	nivel varchar(40) not null ,
	estado varchar(40) not null,
	constraint pk_nivel_formacion primary key (nivel)
);
create table ejercicio.programa(
	codigo varchar (50) not null,
	version varchar (40) not null,
	nombre varchar (500) not null,
	sigla varchar (40) not null,
	estado varchar (40) not null,
	nivel varchar (40) not null,
	constraint pk_programa primary key (codigo_programa, version_programa),
	constraint FK_nivel_formacion foreign key (nivel) references ejercicio.nivel_formacion (nivel) on update cascade on delete restrict
);
create table ejercicio.Planeacion(
	codigo varchar (40) not null, 
	estado varchar(40) not null,
	fecha date not null,
	constraint pk_Planeacion primary key (codigo)
);
create table ejercicio.competencia(
	codigo_competencia varchar (50) not null, 
	denominacion varchar (1000) not null,
	codigo_programa varchar(50) not null,
	version_programa varchar (40) not null,
	constraint pk_competencia primary key (codigo_competencia, codigo_programa, version_programa),
	constraint FK_programa foreign key (codigo_programa, version_programa) references ejercicio.programa (codigo, version) on update cascade on delete restrict
);
create table ejercicio.resultado_aprendizaje(
	codigo_resultado varchar (40) not null, 
	denominacion varchar (1000) not null,
	codigo_competencia varchar(50) not null,
	codigo_programa varchar (50) not null,
	version_programa varchar (40) not null,
	constraint pk_resultado_aprendizaje primary key (codigo_resultado,codigo_competencia, codigo_programa, version_programa),
	constraint FK_competencia foreign key (codigo_competencia, codigo_programa, version_programa) references ejercicio.competencia (codigo_competencia, codigo_programa, version_programa) on update cascade on delete restrict
);
create table ejercicio.planeacion_trimestre(
	codigo_resultado varchar (40) not null,
	codigo_competencia varchar (50) not null, 
	codigo_programa varchar (50) not null,
	version_programa varchar (40) not null,
	sigla_jornada varchar (20) not null,
	nivel varchar (40) not null,
	nombre_trimestre int4 not null,
	codigo_planeacion varchar (40) not null,
	constraint pk_planeacion_trimestre primary key (codigo_resultado, codigo_competencia, codigo_programa, version_programa, sigla_jornada,nivel, nombre_trimestre,codigo_planeacion),
	constraint FK_resultado_aprendizaje foreign key (codigo_resultado, codigo_competencia, codigo_programa, version_programa) references ejercicio.resultado_aprendizaje (codigo_resultado, codigo_competencia, codigo_programa, version_programa) on update cascade on delete restrict,
	constraint FK_trimestre foreign key (sigla_jornada,nivel,nombre_trimestre) references ejercicio.trimestre (sigla_jornada,nivel,nombre_trimestre) on update cascade on delete restrict,
	constraint FK_Planeacion foreign key (codigo_planeacion) references ejercicio.Planeacion (codigo) on update cascade on delete restrict
);
create table ejercicio.actividad_planeacion(
	codigo_resultado varchar (40) not null,
	codigo_competencia varchar (50) not null,
	codigo_programa varchar (50) not null,
	version_programa varchar (40) not null,
	sigla_jornada varchar (20) not null,
	nivel varchar (40) not null,
	nombre_trimestre int4 not null,
	nombre_fase varchar (40) not null,
	codigo_proyecto varchar (40) not null,
	numero_actividad int4 not null,
	codigo_planeacion varchar (40) not null,
	constraint pk_actividad_planeacion primary key (codigo_resultado,codigo_competencia,codigo_programa,version_programa,sigla_jornada,nivel,nombre_trimestre,nombre_fase,codigo_proyecto,numero_actividad,codigo_planeacion),
	constraint FK_planeacion_trimestre foreign key (codigo_resultado,codigo_competencia, codigo_programa, version_programa, sigla_jornada, nivel, nombre_trimestre, codigo_planeacion) references ejercicio.planeacion_trimestre (codigo_resultado,codigo_competencia, codigo_programa, version_programa, sigla_jornada, nivel, nombre_trimestre, codigo_planeacion)on update cascade on delete restrict,
	constraint FK_actividad_proyecto foreign key (numero_actividad, nombre_fase,codigo_proyecto) references ejercicio.actividad_proyecto (numero_actividad, nombre_fase,codigo_proyecto) on update cascade on delete restrict
);

