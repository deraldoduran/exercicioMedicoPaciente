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

INSERT INTO medico(crm, nome, endereço, telefone, especialidade) VALUES (18739, 'Elias', 'Rua X', '8738-1221', 'Pediatria'),
(7646, 'Ana', 'Av Z', '7829-1233', 'Obstetricia'),(39872, 'Pedro', 'Tv H', '9888-2333', 'Oftalmologia');

INSERT INTO paciente(nome, endereço, telefone) VALUES('João', 'Rua 1', '9809-9756'),
('José', 'Rua B', '3621-8978'),('Maria', 'Rua 10', '4567-9872'),('Joana', 'Rua J', '3343-9889');

INSERT INTO convenio(codconv, nome) VALUES (189, 'Cassi'),
(232, 'Unimed'),(454, 'Santa Casa'), (908,'Copasa'), (435, 'São Lucas');

ALTER TABLE atende ADD COLUMN convenio integer;

ALTER TABLE atende DROP CONSTRAINT atende_fkey2;

INSERT INTO atende(crm, convenio) VALUES (18739, 189),
(18739, 908),(7646, 232), (39872, 189);

ALTER TABLE consulta DROP CONSTRAINT consulta_fkey2;

ALTER TABLE possui DROP CONSTRAINT possui_fkey2;

ALTER TABLE possui ADD COLUMN convenio integer;

INSERT INTO possui(tipo, vencimento, paciente, convenio) VALUES ('E', '31/12/2016', 4, 435), ('S', '31/12/2015', 1, 232);
