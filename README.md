# BdCementerio
Codigos de la Base de datos
CREACION DE TABLAS

CREATE TABLE Propietario(
IdPropietario int not null auto_increment,
CedulaPropietario int(10) unsigned zerofill not null,
NombresPropietario varchar(50) not null,
ApellidosPropietario varchar(50) not null,
FechaDeNacimiento date not null,
DireccionPropietario varchar(50) not null,
Telefono1 int (10) unsigned zerofill not null,
Telefono2 int (10) unsigned zerofill,
Primary key(IdPropietario)
);
#--------------------------------------------
CREATE TABLE Provincia(
IdProvincia int not null auto_increment,
NombresProvincia varchar(50) not null,
Primary key(IdProvincia)
);
#----------------------------------------------
CREATE TABLE PersonalExterno(
IdPersonalExterno int not null auto_increment,
CedulaPersonalExterno int(10) unsigned zerofill not null,
NombresPersonalExterno varchar(50) not null,
ApellidosPersonalExterno varchar(50) not null,
CargoPersonalExterno varchar(50) not null,
Primary key(IdPersonalExterno)
);

#------------------------------------------
CREATE TABLE Personal(
IdPersonal int not null auto_increment,
CedulaPersonal int(10) unsigned zerofill not null,
NombresPersonal varchar(50) not null,
ApellidosPersonal varchar(50) not null,
TipoPersonal varchar(50) not null,
DireccionPersonal varchar (50) not null,
TelefonoPersonal int (10) unsigned zerofill not null,
Primary key(IdPersonal)
);
#-----------------------------------------
CREATE TABLE Administrativo(
IdAdministrativo int not null auto_increment,
CargoAdministrativo varchar(50) not null,
Primary key(IdAdministrativo)
);
#----------------------------------------
CREATE TABLE Operativo(
IdOperativo int not null auto_increment,
CargoOperativo varchar(50) not null,
Primary key(IdOperativo)
);

#---------------------------------------
CREATE TABLE Fallecimiento(
IdFallecido int not null auto_increment,
NombresFallecido varchar(50) not null,
ApellidosFallecido varchar(50) not null,
CausaDeMuerte varchar(50) not null,
FechaFallecimiento date not null,
Primary key(IdFallecido)
);
#--------------------------------------------
CREATE TABLE Canton(
IdCanton int not null auto_increment,
NombreCanton varchar(50) not null,
IdProvincia int not null,
IdPropietario int not null,
Primary key(IdCanton),
Foreign Key (IdProvincia) references Provincia (IdProvincia),
Foreign Key (IdPropietario) references Propietario (IdPropietario)
);
#--------------------------------------------
CREATE TABLE Cementerio(
IdCementerio int not null auto_increment,
NombresCementerio varchar(50) not null,
DireccionCementerio varchar(50) not null,
IdCanton int not null,
Primary key(IdCementerio),
Foreign Key (IdCanton) references Canton (IdCanton)
);
#------------------------------------------
CREATE TABLE Manzana(
IdManzana int not null auto_increment,
NombreManzana varchar(50) not null,
IdCementerio int not null,
Primary key(IdManzana),
Foreign Key (IdCementerio) references Cementerio (IdCementerio)
);
#---------------------------------
CREATE TABLE Boveda(
IdBoveda int not null auto_increment,
TipoDeEstructura varchar(50) not null,
IdManzana int not null,
IdPropietario int not null,
Primary key(IdBoveda),
Foreign Key (IdManzana) references Manzana (IdManzana),
Foreign Key (IdPropietario) references Propietario (IdPropietario)
);

#--------------------------------------------
CREATE TABLE Tramite(
IdTramite int not null auto_increment,
TipoTramite varchar(50) not null,
FechaTramite date not null,
IdCanton int not null,
IdPersonal int not null,
IdPersonalExterno int,
IdBoveda int not null,
IdPropietario int not null,
Primary key(IdTramite),
Foreign Key (IdCanton) references Canton (IdCanton),
Foreign Key (IdPersonal) references Personal (IdPersonal),
Foreign Key (IdPersonalExterno) references PersonalExterno (IdPersonalExterno),
Foreign Key (IdBoveda) references Boveda (IdBoveda),
Foreign Key (IdPropietario) references Propietario (IdPropietario)
);

#-----------------------------------------
CREATE TABLE Pago(
IdPago int not null auto_increment,
TipoPago varchar (20) not null,
Fecha date not null,
ValorPago float not null default 00.00,
IdTramite int not null,
IdFallecido int not null,
Primary key(IdPago),
Foreign Key (IdTramite) references Tramite (IdTramite),
Foreign Key (IdFallecido) references Fallecimiento (IdFallecido)
);
-------------------------------------------------------------------
CREATE TABLE Certificado(
IdCertificado int not null auto_increment,
FechaCertificado date not null,
IdPago int(10) not null,
IdTramite int(10) not null,
IdPersonal int(10) not null,
IdFallecido int(10) not null,
Primary key(IdCertificado),
Foreign Key (IdPago) references Pago (IdPago),
Foreign Key (IdTramite) references Tramite (IdTramite),
Foreign Key (IdFallecido) references Fallecimiento (IdFallecido)
);

#----------------------------------------------------------
CREATE TABLE Incidente(
IdIncidente int not null auto_increment,
TipoIncidente varchar (50) not null,
FechaIncidente date not null,
IdBoveda int not null,
IdCertificado int not null,
Primary key(IdIncidente),
Foreign Key (IdBoveda) references Boveda (IdBoveda),
Foreign Key (IdCertificado) references Certificado (IdCertificado)
);


