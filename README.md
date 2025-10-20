# University-Data-System-OOP
Projeto de Desenvolvimento de Sistemas Orientado a Objetos focado na modelagem e gestão eficiente dos dados acadêmicos e administrativos de uma grande instituição de ensino superior.

## 1. Introdução e Visão Geral da Solução (PI - Fase 1)

O projeto apresenta um sistema de gestão de dados para uma universidade, focando no cadastro de pessoas físicas, jurídicas, usuários (alunos e professores) e fornecedores. O objetivo é desenvolver uma estrutura eficiente que permita o registro, atualização e consulta de informações relevantes.

### Objetivos

* Desenvolver um sistema integrado que centralize e automatize o cadastro de alunos, professores e fornecedores, melhorando a eficiência administrativa e a comunicação entre áreas.
* Garantir a segurança e conformidade legal dos dados, fornecendo ferramentas analíticas para a tomada de decisões informadas na gestão acadêmica.

---

## 2. Modelagem de Casos de Uso

A modelagem de casos de uso representa os cenários de cadastro de diferentes tipos de pessoas que interagem com o sistema.

### Diagrama de Caso de Uso

![Diagrama de Caso de Uso do Sistema Universitário](caso_de_uso.png)

* **Atores:** Funcionário, Administrador do Sistema.
* **Casos de Uso Principais:** Cadastrar Pessoa Jurídica, Cadastrar Fornecedores, Cadastrar Pessoa Física, Cadastrar Usuários (Alunos e Professores).

---

## 3. Descrição Detalhada dos Cenários (Casos de Uso)

### 3.1. Caso de Uso 1: Cadastro de Pessoa Física

* **Ator Principal:** Funcionário responsável pelo cadastro.
* **Pré-condição:** O sistema deve estar em funcionamento e o usuário (funcionário) deve estar autenticado.
* **Cenário Principal:** O funcionário acessa o cadastro, preenche os dados obrigatórios, o sistema valida os dados, registra no banco e exibe mensagem de sucesso.
* **Cenário Alternativo 1:** No passo 4, se o CPF informado for inválido ou já estiver cadastrado, o sistema informa o erro e solicita a correção.
* **Cenário Alternativo 2:** No passo 3, se o funcionário não preencher todos os campos obrigatórios, o sistema alerta sobre os campos faltantes e impede a conclusão.
* **Pós-condição:** Os dados da pessoa física são armazenados, ficando disponíveis para consultas e relacionamentos futuros (ex.: vínculo como aluno ou professor).

### 3.2. Caso de Uso 2: Cadastro de Pessoa Jurídica

* **Ator Principal:** Funcionário responsável pelo cadastro.
* **Pré-condição:** O sistema deve estar em funcionamento e o funcionário deve estar autenticado.
* **Cenário Principal:** O funcionário preenche os dados obrigatórios (Razão Social, Nome Fantasia, CNPJ, Endereço, Telefone e E-mail), o sistema valida e registra no banco, exibindo mensagem de sucesso.
* **Cenário Alternativo 1:** Se o CNPJ informado for inválido ou já estiver cadastrado, o sistema informa o erro e solicita a correção.
* **Cenário Alternativo 2:** Se o funcionário não preencher todos os campos obrigatórios, o sistema alerta e impede a conclusão do cadastro.
* **Pós-condição:** Os dados da pessoa jurídica são armazenados, ficando disponíveis para consultas e relacionamentos futuros (ex.: vínculo como fornecedor).

### 3.3. Caso de Uso 3: Cadastro de Usuários (Alunos e Professores)

* **Ator Principal:** Administrador do Sistema.
* **Pré-condição:** O Administrador deve estar autenticado e possuir privilégios de acesso.
* **Cenário Principal (Passos Chave):** O Administrador insere os dados pessoais obrigatórios, seleciona o perfil (Aluno ou Professor), preenche os campos adicionais do perfil. O sistema valida, cria o registro de Pessoa Física e associa o perfil.
* **Cenário Alternativo 1 (Cadastro de Perfil em Pessoa Física existente):** O Administrador localiza uma Pessoa já cadastrada, o sistema disponibiliza apenas os campos específicos para o novo perfil, e associa o perfil ao registro existente.
* **Cenário Alternativo 2 (Campos Obrigatórios não preenchidos):** O sistema detecta os campos ausentes, interrompe a operação e exibe mensagem de erro.
* **Cenário Alternativo 3 (Cadastro duplicado):** O Administrador tenta cadastrar um CPF já presente na base, o sistema rejeita a operação e exibe mensagem de duplicidade.
* **Cenário Alternativo 4 (Permissão insuficiente):** Um usuário sem perfil de Administrador tenta acessar, o sistema bloqueia o acesso e exibe “Acesso negado”.
* **Pós-condição (Sucesso):** Um novo registro de Pessoa Física (quando aplicável) e o respectivo perfil são criados no banco de dados.

### 3.4. Caso de Uso 4: Cadastro de Fornecedor

* **Ator Principal:** Funcionário do Setor Administrativo.
* **Pré-condição:** O funcionário deve estar autenticado e o sistema conectado ao banco de dados.
* **Cenário Principal:** O funcionário insere informações obrigatórias (Razão social, CNPJ, Endereço, Telefone de contato, E-mail e Tipo de fornecimento). O sistema valida, armazena e apresenta mensagem de sucesso.
* **Cenário Alternativo 1 (Dados incompletos):** O sistema exibe uma mensagem de erro informando os campos que ainda precisam ser preenchidos.
* **Cenário Alternativo 2 (CNPJ inválido ou duplicado):** O sistema bloqueia o cadastro e informa o motivo do erro.
* **Pós-condição:** O fornecedor é registrado no sistema e fica disponível para consultas e edições futuras.

---

## 4. Modelagem de Classes Orientada a Objetos

O diagrama de classes ilustra a estrutura das entidades envolvidas no sistema de cadastro.

### 4.1. Diagrama de Classes (Visão Geral)

![Diagrama de Classes - Estrutura Principal](diagrama_classes1.png)
![Diagrama de Classes - Continuação](diagrama_classes2.png)

### 4.2. Classes, Atributos e Métodos (Exemplos)

| Classe | Atributos (Exemplos) | Métodos (Exemplos) |
| :--- | :--- | :--- |
| **Pessoa** | `id:int`, `endereco:string`, `telefone:string`, `email:string` | `validarEmail():bool`, `atualizarContato():void` |
| **Pessoa Fisica** | `cpf:string`, `nome:string`, `dataNascimento:date` | `validarCPF():bool`, `cadastrarPF():void` |
| **Pessoa Juridica** | `cnpj:string`, `razaoSocial:string`, `nomeFantasia:string` | `validarCNPJ():bool`, `cadastrarPJ():void` |
| **Professor** | `siape:string`, `areaAtuacao:string`, `titulacao:string` | `atribuirDisciplina():void`, `consultarTurmas():void` |
| **Aluno** | `matricula:string`, `anoIngresso:int`, `modalidade:string` | `matricularDisciplina():void`, `consultarHistorico():void` |
| **Fornecedor** | `tipoFornecimento:string`, `status:string` | `cadastrarFornecedor():void`, `atualizarFornecedor():void` |

### 4.3. Relacionamentos

* Pessoa é superclasse de Aluno e Professor.
* Curso possui várias Disciplinas.
* Aluno está matriculado em várias Disciplinas.
* Professor ministra várias Disciplinas.

---

## 5. Próximos Passos (Fase 2: Prototipação e Configuração do GitHub)

Esta seção será preenchida na segunda entrega do PI, conforme os requisitos de prototipação das interfaces e a organização dos colaboradores no repositório.
