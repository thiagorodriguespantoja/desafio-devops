
# Instrumentação do Ambiente

Este documento descreve detalhadamente o processo de configuração e operação dos containers `postgres_a`, `postgres_b`, `promtail`, e `loki`. Ele fornece informações suficientes para que outro analista possa replicar o ambiente do zero e realizar operações de backup. Os logs relevantes também estão incluídos para referência.

## 1. Configuração Inicial

### 1.1. PostgreSQL Containers
Os containers `postgres_a` e `postgres_b` foram configurados com as seguintes etapas:

1. Baixar a imagem do PostgreSQL versão 16.3.
2. Configurar os containers para escutar nas portas 5432 em IPv4 e IPv6.
3. Certificar-se de que o diretório do banco de dados contém uma instância do PostgreSQL, caso contrário, inicializar a base de dados.

Logs:
```
2024-08-08 22:06:43 postgres_a  | PostgreSQL Database directory appears to contain a database; Skipping initialization
2024-08-08 22:06:43 postgres_a  | 2024-08-09 01:06:43.242 UTC [1] LOG:  starting PostgreSQL 16.3 (Debian 16.3-1.pgdg120+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 12.2.0-14) 12.2.0, 64-bit
2024-08-08 22:06:43 postgres_a  | 2024-08-09 01:06:43.242 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
...
```

### 1.2. Promtail Container
O `promtail` foi configurado para agregar logs de arquivos em `/var/log/*log` e enviar para o Loki.

Logs:
```
2024-08-08 22:06:43 promtail    | level=info ts=2024-08-09T01:06:43.45397488Z caller=server.go:260 http=[::]:9080 grpc=[::]:45525 msg="server listening on addresses"
2024-08-08 22:06:43 promtail    | level=info ts=2024-08-09T01:06:43.461263751Z caller=main.go:119 msg="Starting Promtail" version="(version=2.4.1, branch=HEAD, revision=f61a4d261)"
...
```

### 1.3. Loki Container
O Loki foi iniciado para coletar e processar logs enviados pelo `promtail`.

Logs:
```
2024-08-08 22:06:43 loki        | 2024-08-09 01:06:43.223494 I | proto: duplicate proto type registered: purgeplan.DeletePlan
2024-08-08 22:06:43 loki        | 2024-08-09 01:06:43.223580 I | proto: duplicate proto type registered: purgeplan.ChunksGroup
...
```

## 2. Procedimentos de Backup

### 2.1. Backup do PostgreSQL
Para realizar o backup do PostgreSQL, siga as instruções abaixo:

1. Identifique o container PostgreSQL em execução (`postgres_a` ou `postgres_b`).
2. Utilize a ferramenta `pg_dump` para gerar o dump do banco de dados.

Exemplo de comando:
```bash
docker exec -t postgres_a pg_dumpall -c -U postgres > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

Logs:
```
2024-08-08 23:11:43 postgres_b  | 2024-08-09 02:11:43.174403447Z caller=checkpoint.go:617 msg="starting checkpoint"
2024-08-08 23:11:43 postgres_b  | 2024-08-09 02:11:43.175389109Z caller=checkpoint.go:342 msg="attempting checkpoint for" dir=/loki/wal/checkpoint.000012
...
```

## 3. Resolução de Problemas

### 3.1. Mensagens de Erro Comuns
Durante a execução dos containers, pode ocorrer a mensagem "invalid length of startup packet". Este erro geralmente indica um problema com a configuração do cliente que está tentando se conectar ao PostgreSQL.

Logs:
```
2024-08-08 22:12:37 postgres_a  | 2024-08-09 01:12:37.666 UTC [97] LOG:  invalid length of startup packet
...
```

### 3.2. Solução de Problemas
1. Verifique a configuração do cliente.
2. Certifique-se de que o cliente esteja utilizando a versão correta do PostgreSQL e parâmetros de conexão.

---

Este documento deve ser atualizado conforme necessário para refletir mudanças no ambiente ou procedimentos.
