# Analytics com Python

Repositório criado para armazenar notebooks de **análise de dados, engenharia de dados e automações em Python**.

---

## Arquivo Read-SQLServer

Este notebook mostra como conectar-se a um banco de dados **SQL Server** usando Python, realizar consultas, listar tabelas e exportar os resultados para Excel e TXT.

---

### Tecnologias utilizadas
- Python 3.11  
- [pyodbc](https://github.com/mkleehammer/pyodbc)  
- [pandas](https://pandas.pydata.org/)  
- [openpyxl](https://openpyxl.readthedocs.io/)  

---

### Passo a passo

#### 1. Instalação das bibliotecas
```python
!pip install pyodbc pandas openpyxl
```
#### 2. Importação
```python
import pyodbc
import pandas as pd
```
#### 3. Parâmetros da conexão
```python
server = "DESKTOP-SEU_SERVIDOR"
database = "AdventureWorksDW2022"
driver = "ODBC Driver 17 for SQL Server"

conn = pyodbc.connect(
    f"DRIVER={{{driver}}};"
    f"SERVER={server};"
    f"DATABASE={database};"
    "Trusted_Connection=yes;"
)

print("Conexão realizada com sucesso!")
```
#### 4. Contar o número de tabelas
```python
cursor = conn.cursor()
cursor.execute("SELECT COUNT(*) FROM sys.tables;")
qtd = cursor.fetchone()[0]
print(f"Esse banco de dados tem {qtd} tabelas.")
```

#### 5. Listar os nomes das tabelas
```python
cursor.execute("SELECT name FROM sys.tables;")
rows = cursor.fetchall()
table_names = [row[0] for row in rows]
table_names
```

#### 6. Criar DataFrame com os nomes
```python
df = pd.DataFrame(table_names, columns=["Tabela"])
df.index = df.index + 1
df
```

#### 7. Exportar resultados
```python
# Excel
df.to_excel("tabelas_sqlserver.xlsx", index=True)
# TXT
df.to_csv("tabelas_sqlserver.txt", index=True, sep="\t")
print("Arquivos gerados com sucesso!")
```
---

```bash
analytics-python/
│── Read-SQLServer.ipynb   # Notebook completo de conexão e consultas
│── tabelas_sqlserver.xlsx # Export Excel 
│── tabelas_sqlserver.txt  # Export TXT
│── README.md              # Este arquivo
```
---

By: Camila Primo