# Sistema de Gestão das Olimpíadas (SGO)

> Trabalho 1 – Projeto de Software | PUC Minas | Prof. João Paulo Carneiro Aramuni

---

## Descrição

O SGO é um sistema para coordenar os diferentes aspectos das Olimpíadas: gerenciamento de competições, inscrição de atletas, alocação de locais e controle de resultados.

---

## Histórias de Usuário

### US01 – Cadastrar Competição
**Como** Comitê Olímpico,  
**quero** cadastrar uma competição informando nome, modalidade, data, horário de início, horário de fim e local,  
**para que** a programação oficial das provas esteja registrada no sistema.

**Critérios de aceitação:**
- O sistema deve exigir nome, modalidade, data, horário de início e horário de fim.
- O status inicial da competição deve ser `AGENDADA`.
- Não deve ser possível cadastrar duas competições com o mesmo nome na mesma data e horário.

---

### US02 – Editar Competição
**Como** Comitê Olímpico,  
**quero** editar os dados de uma competição já cadastrada,  
**para que** correções ou ajustes na programação possam ser feitos sem cancelar a prova.

**Critérios de aceitação:**
- Somente competições com status `AGENDADA` podem ser editadas.
- Alterações de data/horário devem re-verificar conflito de local.

---

### US03 – Listar Competições
**Como** Comitê Olímpico ou Atleta,  
**quero** visualizar a lista de competições cadastradas,  
**para que** eu possa consultar a programação das provas.

**Critérios de aceitação:**
- A listagem deve exibir: nome, modalidade, data, horário, local e status.
- Deve ser possível filtrar por modalidade, data e status.

---

### US04 – Cancelar Competição
**Como** Comitê Olímpico,  
**quero** cancelar uma competição cadastrada,  
**para que** o local seja liberado e os atletas inscritos sejam notificados.

**Critérios de aceitação:**
- O status da competição passa para `CANCELADA`.
- O local alocado é liberado automaticamente.
- O sistema notifica por e-mail os atletas inscritos.

---

### US05 – Cadastrar Atleta
**Como** Comitê Olímpico,  
**quero** cadastrar um atleta informando nome, data de nascimento, sexo, documento e país,  
**para que** ele possa ser inscrito em competições.

**Critérios de aceitação:**
- O documento (CPF ou passaporte) deve ser único no sistema.
- O país do atleta deve estar previamente cadastrado.

---

### US06 – Inscrever Atleta em Competição
**Como** Atleta ou Comitê Olímpico,  
**quero** inscrever um atleta em uma competição,  
**para que** ele possa participar da prova representando seu país.

**Critérios de aceitação:**
- O atleta só pode representar um país por modalidade (US07).
- A competição deve estar com status `AGENDADA`.
- O sistema registra data/hora da inscrição e define status como `PENDENTE`.

---

### US07 – Validar Representação de País
**Como** Sistema,  
**quero** validar que um atleta não represente mais de um país na mesma modalidade,  
**para que** a integridade das regras olímpicas seja garantida.

**Critérios de aceitação:**
- Se o atleta já possui inscrição confirmada em outra competição da mesma modalidade representando país diferente, a nova inscrição é recusada com mensagem de erro clara.

---

### US08 – Cancelar Inscrição
**Como** Atleta ou Comitê Olímpico,  
**quero** cancelar a inscrição de um atleta em uma competição,  
**para que** a vaga fique disponível e o registro seja atualizado.

**Critérios de aceitação:**
- O status da inscrição passa para `CANCELADA`.
- Só é possível cancelar inscrições com status `PENDENTE` ou `CONFIRMADA`.
- O cancelamento só é permitido até 24 h antes da competição.

---

### US09 – Cadastrar Local
**Como** Comitê Olímpico,  
**quero** cadastrar um local informando nome, endereço e capacidade,  
**para que** ele possa ser alocado para competições.

**Critérios de aceitação:**
- Nome e endereço são obrigatórios.
- Capacidade deve ser um número inteiro positivo.

---

### US10 – Alocar Local para Competição
**Como** Comitê Olímpico,  
**quero** alocar um local para uma competição,  
**para que** a prova tenha um espaço físico reservado sem conflitos de horário.

**Critérios de aceitação:**
- O sistema deve verificar automaticamente conflitos de horário (US11).
- Um local só pode abrigar uma competição por vez.
- A alocação registra data/hora da operação.

---

### US11 – Verificar Conflito de Horário
**Como** Sistema,  
**quero** verificar se um local já está ocupado no intervalo solicitado,  
**para que** não haja duas competições simultâneas no mesmo espaço.

**Critérios de aceitação:**
- O sistema verifica sobreposição entre `horarioInicio` e `horarioFim` na mesma data.
- Se houver conflito, a alocação é bloqueada e uma mensagem de erro é retornada.

---

### US12 – Registrar Resultado
**Como** Comitê Olímpico,  
**quero** registrar o resultado de uma competição,  
**para que** os classificados em 1.º, 2.º e 3.º lugar sejam formalizados.

**Critérios de aceitação:**
- Só é possível registrar resultado de competição com status `CONCLUIDA`.
- O sistema define automaticamente as medalhas: ouro, prata e bronze (US13).
- Observações opcionais podem ser adicionadas.

---

### US13 – Definir Vencedor e Classificados
**Como** Sistema,  
**quero** associar automaticamente as medalhas de ouro, prata e bronze aos atletas classificados,  
**para que** o resultado seja consistente com as regras olímpicas.

**Critérios de aceitação:**
- 1.º lugar recebe `OURO`, 2.º recebe `PRATA`, 3.º recebe `BRONZE`.
- A marca (tempo / pontuação) é registrada em cada `Classificação`.

---

### US14 – Consultar Resultados
**Como** Atleta ou Comitê Olímpico,  
**quero** consultar os resultados das competições,  
**para que** eu possa ver os classificados e as marcas registradas.

**Critérios de aceitação:**
- Os resultados exibem: competição, modalidade, local, atletas classificados, medalhas e marcas.
- Deve ser possível filtrar por modalidade, data e país.

---

### US15 – Gerar Relatório de Medalhas
**Como** Comitê Olímpico,  
**quero** gerar um relatório consolidado de medalhas por país,  
**para que** o quadro de medalhas oficial das Olimpíadas seja produzido.

**Critérios de aceitação:**
- O relatório exibe: país, quantidade de ouros, pratas, bronzes e total de medalhas.
- A ordenação padrão é por número de ouros (desempate por pratas, depois bronzes).

---

### US16 – Visualizar Quadro de Medalhas
**Como** Comitê Olímpico,  
**quero** visualizar o quadro de medalhas na tela do sistema,  
**para que** eu possa acompanhar o desempenho dos países em tempo real.

**Critérios de aceitação:**
- O quadro é atualizado automaticamente após cada registro de resultado.
- Exibe bandeira, sigla, nome do país e contagem por tipo de medalha.

---

### US17 – Exportar Relatório
**Como** Comitê Olímpico,  
**quero** exportar o relatório de medalhas em PDF ou Excel,  
**para que** o documento possa ser distribuído e arquivado oficialmente.

**Critérios de aceitação:**
- O arquivo exportado é armazenado no servidor de arquivos (S3/MinIO).
- O sistema notifica por e-mail quando o arquivo estiver disponível para download.
- Formatos suportados: PDF e Excel (.xlsx).

---

## Diagramas

### Diagrama de Caso de Uso
<img width="800px" src="imagens/Diagrama-De-Caso-De-Uso.png"/>

### Diagrama de Classes
<img width="800px" src="imagens/Diagrama-De-Classes.png"/>

### Diagrama de Pacotes
<img width="800px" src="imagens/Diagrama-De-Pacotes.png"/>

### Diagrama de Componentes
<img width="800px" src="imagens/Diagrama-De-Componentes.png"/>

### Diagrama de Implantação
<img width="800px" src="imagens/Diagrama-De-Implantacao.png"/>

---

## Estrutura do Repositório

```
sistema-gestao-olimpiadas/
├── README.md
├── imagens/
│   ├── diagrama-de-caso-de-uso.png
│   ├── diagrama-de-classes.png
│   ├── diagrama-de-pacotes.png
│   ├── diagrama-de-componentes.png
│   └── diagrama-de-implantacao.png
└── codigos/
    ├── diagrama-de-caso-de-uso.puml
    ├── diagrama-de-classes.puml
    ├── diagrama-de-pacotes.puml
    ├── diagrama-de-componentes.puml
    └── diagrama-de-implantacao.puml
```

---

## Tecnologias de Referência

| Camada | Tecnologia |
|---|---|
| Frontend | SPA (React)|
| API Gateway | REST HTTP/JSON |
| Backend | Módulos com interfaces (ICompeticao, IInscricao, IAlocacao, IResultado, IRelatorio) |
| Banco de Dados | PostgreSQL |
| Armazenamento | S3 |
| Notificações | SMTP / SendGrid |
| Autenticação | OAuth2 / JWT |