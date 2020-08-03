# exercicioMedicoPaciente
exercicio FBD


CREATE TABLE IF NOT EXISTS convenio (
	codconv serial not null,
	nome varchar(20),
	
	-- chave primaria
	CONSTRAINT convenio_pkey PRIMARY KEY (codconv)
);

CREATE TABLE IF NOT EXISTS paciente (
	codpac serial not null,
	nome varchar(60),
	endereço varchar(255),
	telefone varchar(25),
	
	--chave primaria
	CONSTRAINT paciente_pkey PRIMARY KEY (codpac)

);

CREATE TABLE IF NOT EXISTS convenio(
	codconv integer,
	nome varchar(60),
	
	--chave primaria
	CONSTRAINT convenio_pkey PRIMARY KEY (codconv)

);

CREATE TABLE IF  NOT EXISTS medico(
	crm integer,
	nome varchar(60),
	endereço varchar(255),
	telefone varchar(20),
	especialidade varchar(20),
	
	CONSTRAINT medico_pkey PRIMARY KEY (crm)

);

CREATE TABLE IF NOT EXISTS consulta (
	codconsulta serial not null,
	dia date,
	horario time,
	porcent integer,
	
	CONSTRAINT consulta_pkey PRIMARY KEY (codconsulta),
	
	CONSTRAINT consulta_fkey FOREIGN KEY (codconsulta)
REFERENCES medico(crm),
	  CONSTRAINT consulta_fkey2 FOREIGN KEY (codconsulta) REFERENCES paciente(codpac)

);

CREATE TABLE IF NOT EXISTS atende(
	crm integer,
	CONSTRAINT atende_fkey FOREIGN KEY (crm)
REFERENCES medico (crm),
	CONSTRAINT atende_fkey2 FOREIGN KEY (crm) REFERENCES convenio(CODCONV)

);

CREATE TABLE IF NOT EXISTS possui(
	tipo varchar(20),
	vencimento date,
	paciente integer,
	
	CONSTRAINT possui_pkey PRIMARY KEY (paciente),
	CONSTRAINT possui_fkey FOREIGN KEY (paciente)
REFERENCES paciente(codpac),
CONSTRAINT possui_fkey2 FOREIGN KEY(paciente) REFERENCES convenio(codconv)
	
);


