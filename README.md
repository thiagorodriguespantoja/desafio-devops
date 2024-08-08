<p align="center">
  <a href="" rel="noopener">
    <img width="200" height="200" src="https://drive.google.com/uc?export=view&id=1svyh9KYiynNx4FhpR22jExg7p0xscrbU" alt="Project logo">
  </a>
</p>


<h3 align="center">Desafio Técnico: Pentaho PDI, Linux e PostgreSQL</h3>


---

## Descrição

Este desafio técnico tem como objetivo avaliar a competência técnica do candidato em um ambiente utilizando Pentaho Data Integration (PDI), Linux e PostgreSQL.


## Objetivo

1. Preparar um ambiente Linux (VM ou WSL) com as ferramentas necessárias (Utilize apenas Windows se houver necessidade).
2. Configurar dois bancos de dados PostgreSQL utilizando scripts fornecidos.
3. Integrar dados entre os dois bancos de dados usando Pentaho PDI, lidando com erros de tipos de dados.
4. Documentar e versionar todo o trabalho no GitHub.
5. Lidar com erros de integração de dados

## Requisitos

### Obrigatórios:
- VM Linux ou WSL no Windows (Utilize apenas Windows se houver necessidade).
- Pentaho Data Integration (PDI)
- PostgreSQL
- GitHub para versionamento
- Scripts SQL fornecidos (backup_a e backup_b)

### Diferenciais:
- Uso de Docker para configurar o ambiente


## Instruções

### 1. Preparação do Ambiente
- Configure uma VM Linux ou use o WSL no Windows (Utilize apenas Windows se houver necessidade).
- Instale as seguintes ferramentas:
  - Pentaho Data Integration (PDI)
  - PostgreSQL
  - Docker (opcional)

### 2. Configuração dos Bancos de Dados
- Criação dos bancos de dados
  - Crie dois bancos de dados banco_a e banco_b
- Execute os scripts SQL fornecidos para configurar os bancos de dados:
  - backup_a.dmp: Criação da tabela consumos_a no banco_a.
  - backup_b.dmp: Criação da tabela consumos_b no banco_b.

### 3. Integração e Manipulação de Dados
- Use Pentaho PDI para transferir os dados da tabela consumos_a para a tabela consumos_b
- Lide com erros de tipos de dados modificados entre os bancos de dados e documente as soluções aplicadas.
  
### 4. Documentação e Entregáveis
- Arquivos KTR:
  - Inclua todos os arquivos KTR utilizados no processo de integração.
- Backups dos Bancos de Dados:
  - Forneça backups finais dos bancos de dados após a integração.
- Fluxograma:
  - Crie um fluxograma detalhado do passo a passo utilizado durante todo o processo.
- GitHub:
  - Versione os arquivos KTR, backups e fluxograma no GitHub.
  - Diferencial: Versione também os contêineres Docker, se utilizados.

## Entrega
- Crie um repositório no GitHub e envie todos os arquivos mencionados acima.
- Forneça o link do repositório ao final do desafio para o e-mail arielle.reis@systock.com.br
- Envie o projeto até o dia 26/07/2024.
- Entregue o desafio mesmo que ainda não tenha concluído.


