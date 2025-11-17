
CREATE TABLE Pessoa (
    id SERIAL PRIMARY KEY, -- id:int, chave primária auto-incrementável
    endereco VARCHAR(255) NOT NULL, -- endereco:string
    telefone VARCHAR(20), -- telefone:string
    email VARCHAR(100) UNIQUE NOT NULL, -- email:string, validarEmail() e UNIQUE
    login VARCHAR(50) UNIQUE NOT NULL, -- login:string
    senha VARCHAR(255) NOT NULL -- senha:string
);

CREATE TABLE Pessoa_Fisica (
    pessoa_id INT PRIMARY KEY,
    cpf VARCHAR(14) UNIQUE NOT NULL, -- cpf:string, validarCPF() e UNIQUE
    rg VARCHAR(20), -- rg:string
    nome VARCHAR(150) NOT NULL, -- nome:string
    dataNascimento DATE, -- dataNascimento:date
    sexo CHAR(1), -- sexo:string
    estadoCivil VARCHAR(20), -- estadoCivil:string
    nomeSocial VARCHAR(150), -- nomeSocial:string
    FOREIGN KEY (pessoa_id) REFERENCES Pessoa(id)
);

CREATE TABLE Pessoa_Juridica (
    cnpj VARCHAR(18) PRIMARY KEY, -- cnpj:string, validarCNPJ()
    razaoSocial VARCHAR(200) NOT NULL, -- razaoSocial:string
    nomeFantasia VARCHAR(150), -- nomeFantasia:string
    inscricaoEstadual VARCHAR(50), -- inscricao Estadual:string
    inscricaoMunicipal VARCHAR(50), -- inscricao Municipal:string
    categoria VARCHAR(100) -- categoria:string
);

CREATE TABLE Administrador (
    pessoa_id INT PRIMARY KEY,
    permissoes VARCHAR(255), -- permissoes:string
    FOREIGN KEY (pessoa_id) REFERENCES Pessoa(id)
);

CREATE TABLE Professor (
    pessoa_id INT PRIMARY KEY,
    siape VARCHAR(20) UNIQUE, -- siape:string
    areaAtuacao VARCHAR(150), -- areaAtuacao:string
    titulacao VARCHAR(100), -- titulacao:string
    regime VARCHAR(50), -- regime:string
    FOREIGN KEY (pessoa_id) REFERENCES Pessoa(id)
);

CREATE TABLE Aluno (
    pessoa_id INT PRIMARY KEY,
    matricula VARCHAR(20) UNIQUE NOT NULL, -- matricula:string
    anoIngresso INT, -- anoIngresso:int
    modalidade VARCHAR(50), -- modalidade:string
    FOREIGN KEY (pessoa_id) REFERENCES Pessoa(id)
);

CREATE TABLE Curso (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL UNIQUE
    -- curso:string (atributo no Aluno/Professor) será resolvido por relacionamento
);

CREATE TABLE Disciplina (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    curso_id INT NOT NULL,
    FOREIGN KEY (curso_id) REFERENCES Curso(id)
);

CREATE TABLE Fornecedor (
    cnpj VARCHAR(18) PRIMARY KEY, -- Chave de Pessoa Jurídica
    tipoFornecimento VARCHAR(100), -- tipoFornecimento:string
    status VARCHAR(20), -- status:string
    contatoResponsavel VARCHAR(100), -- contato Responsavel:string
    observacoes TEXT, -- observacoes:string
    FOREIGN KEY (cnpj) REFERENCES Pessoa_Juridica(cnpj)
);

CREATE TABLE Professor_Disciplina (
    professor_id INT NOT NULL,
    disciplina_id INT NOT NULL,
    PRIMARY KEY (professor_id, disciplina_id),
    FOREIGN KEY (professor_id) REFERENCES Professor(pessoa_id),
    FOREIGN KEY (disciplina_id) REFERENCES Disciplina(id)
);

CREATE TABLE Aluno_Disciplina (
    aluno_id INT NOT NULL,
    disciplina_id INT NOT NULL,
    PRIMARY KEY (aluno_id, disciplina_id),
    FOREIGN KEY (aluno_id) REFERENCES Aluno(pessoa_id),
    FOREIGN KEY (disciplina_id) REFERENCES Disciplina(id)
);
