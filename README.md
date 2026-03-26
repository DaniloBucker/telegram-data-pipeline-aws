# Telegram Data Pipeline (AWS)

Pipeline de dados serverless para ingestão, processamento e análise de mensagens do Telegram utilizando serviços da AWS.

---

## 🏗️ Arquitetura
```
Telegram → API Gateway → Lambda → S3 (RAW)  
→ Lambda ETL → S3 (ENRICHED - Parquet)  
→ Athena
```
---

## ⚙️ Tecnologias utilizadas

- Python  
- AWS Lambda  
- Amazon S3  
- Amazon API Gateway  
- Amazon EventBridge  
- Amazon Athena  
- PyArrow  

---

## 🔄 Pipeline de Dados

### 🔹 Ingestão
- Webhook do Telegram envia mensagens
- API Gateway recebe os dados
- Lambda salva JSON no S3 (RAW)

### 🔹 Transformação (ETL)
- Processamento diário (D-1)
- Conversão JSON → Parquet
- Particionamento por `context_date`

### 🔹 Consumo
- Consulta via SQL no Athena
- Tabela externa particionada

---

## 📊 Análises realizadas

- Volume de mensagens por dia  
- Usuários mais ativos  
- Horário de maior atividade  

---

## 🧠 Insights

- Poucos usuários concentram a maioria das mensagens  
- Existem horários com pico de atividade  
- Particionamento reduz custo no Athena  

---

## ⚠️ Problemas encontrados (e soluções)

- Partições não apareciam no Athena  
  → resolvido com `MSCK REPAIR TABLE`

- ETL ignorava dias sem dados  
  → identificado como falha silenciosa

---

## 📁 Estrutura do projeto

```
telegram-data-pipeline-aws/
│
├── sql/
│ ├── create_table.sql
│ ├── queries.sql
│
├── lambda/
│ └── lambda_function.py
│
├── images/
│ ├── architecture.png
│ ├── athena_query.png
│ ├── s3_partitions.png
│
├── docs/
│ └── explanation.md
│
├── README.md
├── .gitignore
└── LICENSE
```
