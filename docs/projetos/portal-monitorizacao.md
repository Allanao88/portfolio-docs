# Portal de Monitorias Online

Painel centralizado para monitorização de infraestrutura de bases de dados (MySQL, SQL Server), pipelines de dados (Apache Airflow), gestão de tickets (RedMine) e produtividade operacional (Íris).

## 📂 Arquitetura do Projeto

O projeto adota uma arquitetura modular, separando as responsabilidades entre Frontend (Vanilla JS/HTML/CSS) e Backend (FastAPI). Esta estrutura facilita a manutenção, o debug e a escalabilidade de novas integrações.

meu_painel_dba/
├── .env                     # Variáveis de ambiente com credenciais (não versionado)
├── requirements.txt         # Dependências Python (FastAPI, conectores de BD)
├── README.md                # Documentação do projeto
│
├── backend/
│   ├── main.py              # Maestro da API (Entrypoint FastAPI)
│   ├── database.py          # Conectores de BD (MySQL, SQL Server, PostgreSQL)
│   └── routers/             # Rotas modulares separadas por contexto
│       ├── monitoria.py     # Infraestrutura DBA
│       ├── airflow.py       # Pipelines de Dados
│       ├── redmine.py       # Gestão de Tickets
│       └── iris.py          # Produtividade
│
└── frontend/
    ├── css/
    │   └── style.css        # Estilos globais (Dark/Light Mode e layouts)
    ├── index.html           # Portal/Menu inicial de navegação
    ├── monitoria.html       # Visualização da Infraestrutura
    ├── airflow.html         # Visualização do Airflow
    ├── redmine.html         # Visualização do RedMine
    └── iris.html            # Visualização do Íris

⚙️ Configuração do Ambiente Local
1 - Aceda à pasta do projeto:
Abra o terminal e navegue até ao diretório raiz do projeto.

2 - Crie e ative o ambiente virtual Python:
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate

3 - Instale as dependências:
    pip install -r requirements.txt

4 - Configure o .env:
Crie um ficheiro .env na raiz do projeto com as suas credenciais de acesso às bases de dados. As variáveis necessárias incluem credenciais para MANAGER, ZABBIX, HULK, UNIFICADA e AIRFLOW.

🚀 Executando o Projeto
1 - Inicie o Backend (FastAPI):
A partir da raiz do projeto, navegue para a pasta backend e inicie o Uvicorn:
    cd backend
    uvicorn main:app --reload
A API estará disponível localmente em: http://127.0.0.1:8000

2 - Inicie o Frontend:
Basta abrir o ficheiro frontend/index.html no seu navegador web, ou utilizar uma extensão como o Live Server do VS Code para ter o hot-reload visual.

🐧 Notas para Deploy em CentOS
Para o deploy do backend na sua máquina virtual CentOS, certifique-se de cumprir os seguintes pré-requisitos ao nível do Sistema Operativo antes de executar o pip install -r requirements.txt:

.Dependências de compilação (PostgreSQL e MySQL):
Pacotes base necessários para compilar as bibliotecas de conexão.
    sudo yum install gcc python3-devel postgresql-devel

.Driver ODBC (Para o SQL Server / Zabbix / RedMine / Íris):
É estritamente obrigatório instalar o msodbcsql17 e o unixODBC-devel da Microsoft no CentOS para que o pacote pyodbc consiga comunicar adequadamente com as instâncias SQL Server.

🛠️ Tecnologias Utilizadas
- Backend: Python 3, FastAPI, Uvicorn
- Conectores: PyMySQL (MySQL), PyODBC (SQL Server), Psycopg2 (PostgreSQL)
- Frontend: HTML5, CSS3 (Variáveis nativas para temas), JavaScript (Vanilla fetch API)
