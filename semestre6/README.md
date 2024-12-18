### Sistema de Previsão e Qualificação de Ativos Financeiros com Machine Learning - SPC Grafeno
6° Semestre - 02/2024

Parceiro Acadêmico: SPC Grafeno

## 💻 Nossa proposta
Propomos uma solução inovadora para criar produtos financeiros utilizando aprendizado de máquina, com foco em análise de dados, privacidade e valor estratégico.
- Análise de Dados e Dashboards: Desenvolvimento de dashboards interativos e aplicação de análises estatísticas para identificar padrões e oportunidades.
- Gestão de Usuários: CRUD para usuários e perfis personalizados, garantindo acesso seguro e controle.
- Modelo de Machine Learning: Preparação do banco de dados e treinamento de um modelo avançado para prever tendências, mitigar riscos e qualificar ativos financeiros.
- Visualização e Indicadores: Área para explorar datasets e monitorar o desempenho do modelo.
- Privacidade e Compliance: Coleta de consentimento expresso, acesso e edição de dados pessoais, e exportação de dados em formatos seguros (JSON/CSV), garantindo conformidade legal.

---

## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

 - **Desenvolvimento Backend com Django**: Criação e manutenção de APIs, autenticação de usuários, e manipulação de dados em um banco de dados relacional (PostgreSQL), garantindo a eficiência e segurança do sistema.
  
- **Desenvolvimento Frontend com Vue.js**: Construção de interfaces interativas e responsivas com Vue.js, proporcionando uma experiência de usuário ágil e moderna, além de integração eficaz com o backend.
  
- **Banco de Dados Relacional e NoSQL**: Experiência com PostgreSQL para dados principais e MongoDB para armazenar logs e chaves, gerenciando dados de diferentes tipos com eficiência.
  
- **Integração com MinIO**: Implementação de backup automatizado de dados e armazenamento seguro em MinIO, utilizando integração com soluções de armazenamento em nuvem para garantir a segurança dos dados.
  
- **Automação de Tarefas com Celery**: Criação de tarefas assíncronas para execução de backups periódicos, melhorando a performance e escalabilidade do sistema sem impactar a experiência do usuário.
  
- **Desenvolvimento de APIs com FastAPI**: Criação de servidores rápidos e eficientes para integrações de Machine Learning, otimizando a resposta do sistema e garantindo alta performance.
  
- **Gerenciamento de Contêineres com Docker**: Uso de Docker para orquestrar múltiplos serviços, como bancos de dados e servidores, com configuração de containers via Docker Compose, facilitando a escalabilidade e o gerenciamento de dependências.

---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

 - **Resolução de Problemas**: Capacidade de identificar e resolver questões técnicas complexas, como a integração de diferentes tecnologias e soluções de backups, mantendo o sistema estável e eficiente.

  - **Gerenciamento de Tempo**: Habilidade para coordenar tarefas e projetos simultâneos, organizando o trabalho de forma eficiente e cumprindo prazos com qualidade.

  - **Trabalho em Equipe**: Colaboração eficaz com outros desenvolvedores e stakeholders, garantindo a integração e o alinhamento das partes do sistema para alcançar os objetivos do projeto.

  - **Comunicação Técnica**: Capacidade de explicar de forma clara e objetiva soluções técnicas, facilitando a compreensão de colegas e stakeholders sobre decisões e implementações feitas no sistema.

  - **Adaptabilidade**: Flexibilidade para aprender e aplicar novas tecnologias conforme as necessidades do projeto, como o uso de Vue.js e FastAPI, adaptando-se a diferentes ferramentas e metodologias.

  - **Atenção aos Detalhes**: Habilidade para garantir a precisão na implementação de funcionalidades e a integridade dos dados, especialmente em processos de backup e segurança, assegurando a confiança no sistema.

---
## Contribuições Individuais
<details>
<summary><b>Gestão Segura e Organizada de Usuários com Criptografia e Registro de Ações</b></summary>
<br>
<p></p>
  
```python
class ActionLog:
    def __init__(self, user_id, action_type, logs):
        self.user_id = user_id
        self.action_type = action_type
        self.logs = logs
        self.collection = self.get_collection()

    def get_collection(self):
        collections = sorted(logs_db.list_collection_names(), reverse=True)
        last_collection_name = next((c for c in collections if c.startswith("ActionLog_")), None)

        if not last_collection_name or logs_db[last_collection_name].count_documents({}) >= 10000:
            new_collection_name = f"ActionLog_{len(collections) + 1}"
            return logs_db[new_collection_name]
        else:
            return logs_db[last_collection_name]

    def save(self):
        action_log = {
            'id': str(uuid.uuid4()),
            'user_id': self.user_id,
            'action_type': self.action_type,
            'action_date': timezone.now(),
            'logs': self.logs
        }
        self.collection.insert_one(action_log)


class UserManager(BaseUserManager):
    def create_user(self, username, email, password=None, **extra_fields):
        if not email:
            raise ValueError("O usuário deve ter um email")
        if not username:
            raise ValueError("O usuário deve ter um nome de usuário")

        email = self.normalize_email(email)
        user = self.model(username=username, email=email, **extra_fields)
        if password:
            user.set_password(password)
        user.save(using=self._db)
        return user

    def create_superuser(self, username, email, password=None, **extra_fields):
        extra_fields.setdefault("is_staff", True)
        extra_fields.setdefault("is_superuser", True)
        return self.create_user(username, email, password, **extra_fields)


class User(AbstractBaseUser):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    email = models.EmailField(unique=True, max_length=255)
    username = models.CharField(unique=True, max_length=255)
    first_name = models.CharField(max_length=255)
    last_name = models.CharField(max_length=255)
    password = models.CharField(max_length=255)
    cpf = models.CharField(max_length=255, unique=True)
    contato = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    last_login = models.DateTimeField(null=True, blank=True)

    # Django Admin
    is_admin = models.BooleanField(default=False)
    is_staff = models.BooleanField(default=False)
    is_superuser = models.BooleanField(default=False)

    objects = UserManager()

    USERNAME_FIELD = 'username'
    REQUIRED_FIELDS = ['email']

    def save(self, *args, **kwargs):
        is_update = self.__class__.objects.filter(pk=self.pk).exists()
        
        if is_update and 'update_fields' not in kwargs:
            kwargs['update_fields'] = ['updated_at']

        encryption_key = Fernet.generate_key()
        encryption_key_base64 = base64.urlsafe_b64encode(encryption_key).decode()
        fernet = Fernet(encryption_key)
        
        self.email = fernet.encrypt(self.email.encode())
        self.first_name = fernet.encrypt(self.first_name.encode())
        self.last_name = fernet.encrypt(self.last_name.encode())
        self.cpf = fernet.encrypt(self.cpf.encode())
        self.contato = fernet.encrypt(self.contato.encode())
        super().save(*args, **kwargs)

        encrypt_db.userEncrypt.update_one(
            {'user_id': str(self.id)},
            {'$set': {'key': encryption_key_base64}},
            upsert=True
        )

        action_type = "update" if is_update else "register"
        log_message = "User data updated" if is_update else "User register"
        ActionLog(user_id=str(self.id), action_type=action_type, logs=log_message).save()

    def login(self):
        ActionLog(user_id=str(self.id), action_type="login", logs="User logged in").save()

    def has_perm(self, perm, obj=None):
        return self.is_superuser

    def has_module_perms(self, app_label):
        return self.is_superuser

    def decrypt_data(self):
        try:
            user_encryption_data = encrypt_db.userEncrypt.find_one({'user_id': str(self.id)})
            if not user_encryption_data:
                return None
            
            encryption_key = user_encryption_data['key']
            encryption_key = base64.urlsafe_b64decode(encryption_key)
            fernet = Fernet(encryption_key)

            decrypted_data = {
                'email': self._decrypt_field(fernet, self.email),
                'username': self.username,
                'first_name': self._decrypt_field(fernet, self.first_name),
                'last_name': self._decrypt_field(fernet, self.last_name),
                'cpf': self._decrypt_field(fernet, self.cpf),
                'contato': self._decrypt_field(fernet, self.contato),
            }
            return decrypted_data
        except Exception as e:
            return {"detail": str(e)}

    def _decrypt_field(self, fernet, encrypted_message):
        if encrypted_message.startswith("b'") and encrypted_message.endswith("'"):
            encrypted_message = encrypted_message[2:-1]
        decrypted_message = fernet.decrypt(encrypted_message.encode()).decode()
        return decrypted_message
```
<p>Este código implementa um sistema de gerenciamento de usuários com dados sensíveis criptografados, armazenados em um banco de dados PostgreSQL, enquanto as chaves de criptografia são salvas em uma coleção MongoDB separada para maior segurança. O processo inclui:

- Criação e Atualização de Usuários: Os dados sensíveis do usuário (e-mail, CPF, etc.) são criptografados usando a biblioteca Fernet, com a chave única de criptografia armazenada no MongoDB.
- Registro de Logs de Ações: Cada ação relevante (registro, atualização, login) é documentada em uma coleção MongoDB separada, ActionLog, que organiza os logs em coleções rotativas para manter eficiência e rastreabilidade.
- Descriptografia Segura: Os dados criptografados podem ser acessados de forma segura com a chave correspondente armazenada no MongoDB.
Essa arquitetura combina o PostgreSQL para dados relacionais e o MongoDB para gerenciar chaves e logs, garantindo segurança, rastreabilidade e flexibilidade.</p>
</details>

<details>
<summary><b>Configuração de Ambiente com Docker Compose</b></summary>
<br>

```yml
version: '3.8'

services:
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: mydatabase
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"
    depends_on:
      - db

  mongodb:
    image: mongo:5
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongo_user
      MONGO_INITDB_ROOT_PASSWORD: mongo_password
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db
    command: mongod --auth --dbpath /data/db --bind_ip_all

  mongo-express:
    image: mongo-express
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: mongo_user
      ME_CONFIG_MONGODB_ADMINPASSWORD: mongo_password
      ME_CONFIG_MONGODB_SERVER: mongodb
    ports:
      - "8081:8081"
    depends_on:
      - mongodb

  minio:
    image: minio/minio
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
    command: server /data --console-address ":9001"
    ports:
      - "9000:9000"
      - "9001:9001"
    volumes:
      - minio_data:/data

  redis:
    image: redis:latest
    ports:
      - "6379:6379"

  celery:
    build: .
    command: celery -A backend worker -l info -E
    volumes:
      - ./app:/app
    depends_on:
      - redis
      - db
      - mongodb
      - minio
    environment:
      - DJANGO_SETTINGS_MODULE=backend.settings

  celery-beat:
    build: .
    command: celery -A backend beat -l info
    volumes:
      - ./app:/app
    depends_on:
      - redis
      - db

  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./app:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
      - mongodb
      - redis
      - minio

volumes:
  postgres_data:
  mongo_data:
  minio_data:
```
<p>
Neste trabalho, foi utilizado o Docker Compose para orquestrar a criação de um ambiente de desenvolvimento robusto e escalável. O arquivo docker-compose.yml define os seguintes serviços essenciais:

PostgreSQL: A imagem postgres:13 foi configurada com variáveis de ambiente para o banco de dados, nome de usuário e senha, garantindo a persistência de dados com um volume dedicado. Isso proporciona um banco de dados relacional para armazenamento de informações da aplicação.

PgAdmin: Utilizou-se a imagem dpage/pgadmin4 para facilitar o gerenciamento do PostgreSQL, permitindo o acesso via navegador. Este serviço depende do banco de dados PostgreSQL e é acessado pela porta 5050.

MongoDB: A imagem mongo:5 foi configurada com autenticação ativada. Esse banco NoSQL é utilizado para armazenar dados não estruturados, com a persistência garantida por meio de volumes dedicados.

MinIO: Para simular um armazenamento em nuvem compatível com o Amazon S3, foi configurado o MinIO com a imagem minio/minio. Este serviço é útil para o armazenamento de arquivos, com acesso via porta 9000.

Redis: O Redis foi configurado com a imagem redis:latest, oferecendo cache e suporte para filas de tarefas, essenciais para a performance da aplicação.

Celery: O Celery foi configurado em dois containers: um para o worker, que processa tarefas assíncronas, e outro para o beat, que gerencia tarefas agendadas. Ambos os serviços dependem do Redis para o gerenciamento de filas e do PostgreSQL para o banco de dados.

Além disso, o serviço Web foi configurado para executar a aplicação Django, com o código da aplicação sendo montado diretamente no container. O servidor web é exposto na porta 8000.

Com essa configuração, foi possível criar um ambiente de desenvolvimento completo, integrando bancos de dados relacionais e NoSQL, armazenamento de arquivos, cache e filas de tarefas assíncronas, garantindo a flexibilidade e escalabilidade necessárias para o desenvolvimento de aplicações web.
</p>
</details>

<details>
<summary><b>Modelo para Gestão de Termos LGPD e Registro de Aprovações de Usuários</b></summary>
<br>

```python
class LGPDTermItem(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    title = models.CharField(max_length=100, unique=True)
    content = models.TextField(blank=True)

    def __str__(self):
        return self.title


class LGPDGeneralTerm(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    title = models.CharField(max_length=100, unique=True)
    content = models.TextField()
    term_itens = models.ManyToManyField(LGPDTermItem, blank=True, related_name="general_terms")
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title


class LGPDUserTermApproval(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    general_term = models.ForeignKey('LGPDGeneralTerm', on_delete=models.CASCADE)
    items_term = models.ForeignKey('LGPDTermItem', on_delete=models.CASCADE, null=True)
    approval_date = models.DateTimeField(auto_now_add=True)
    logs = models.TextField()

    def __str__(self):
        return f"Aprovação do {self.user.username}"
```
<p>
Esse código foi projetado para lidar com termos e itens opcionais, garantindo conformidade com a LGPD (Lei Geral de Proteção de Dados) e registrando aprovações de forma segura e organizada.

Modelos Base:

- LGPDTermItem: Representa itens opcionais que podem ser associados a termos gerais. Cada item tem um título único e um conteúdo descritivo.
LGPDGeneralTerm: Refere-se aos termos gerais que os usuários precisam aceitar. Ele pode ter vários itens opcionais vinculados, o que permite uma personalização maior ao lidar com diferentes condições ou cláusulas.
Relação com o Usuário:

- GPDUserTermApproval: Este modelo registra as aprovações dos termos por parte dos usuários. Ele vincula o usuário, o termo geral aceito e, opcionalmente, um item específico. Além disso, armazena a data da aprovação e os logs, que podem ser usados para auditorias ou histórico.
Funcionalidade e Segurança:

- Todas as entradas possuem um identificador único (UUID) para evitar conflitos.
As aprovações são vinculadas diretamente aos usuários, garantindo rastreabilidade.
Logs de ações permitem registrar informações adicionais sobre a aprovação, como contexto ou detalhes específicos.

Em resumo, esse modelo organiza termos e itens opcionais, assegura o registro das aprovações e facilita a rastreabilidade e auditoria, contribuindo para uma gestão clara e segura das obrigações relacionadas à proteção de dados.
</p>
</details>

<details>
<summary><b>Configuração de Tarefas do Celery para Backup e Armazenamento no MinIO</b></summary>
<br>

```python
import os
import subprocess
from celery import shared_task
from minio import Minio
from datetime import datetime
import psycopg2
from pymongo import MongoClient
import json
import logging


MINIO_CLIENT = Minio(
    'minio:9000',
    access_key='minioadmin',
    secret_key='minioadmin',
    secure=False
)


@shared_task
def backup_postgres():
    timestamp = datetime.now().strftime('%Y%m%d%H%M%S')

    try:
        postgres_backup_file = f'/tmp/postgres_backup_{timestamp}.sql'
        logging.info("Iniciando backup do PostgreSQL...")

        connection = psycopg2.connect(
            dbname="mydatabase",
            user="myuser",
            password="mypassword",
            host="db",
            port="5432"
        )
        cursor = connection.cursor()

        cursor.execute("SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';")
        tables = cursor.fetchall()

        with open(postgres_backup_file, 'w') as backup_file:
            for table in tables:
                table_name = table[0]
                logging.info(f"Realizando backup da tabela {table_name}...")
                cursor.copy_expert(f"COPY {table_name} TO STDOUT WITH CSV HEADER", backup_file)

        logging.info(f"Backup do PostgreSQL concluído.")
        upload_to_minio(postgres_backup_file, f'backups/postgres/{timestamp}.sql')

        cursor.close()
        connection.close()

    except Exception as e:
        logging.error(f"Erro ao fazer backup do PostgreSQL: {e}")

    if os.path.exists(postgres_backup_file):
        os.remove(postgres_backup_file)
        logging.info(f"Arquivo temporário {postgres_backup_file} removido.")


@shared_task
def backup_mongo_logs():
    timestamp = datetime.now().strftime('%Y%m%d%H%M%S')

    try:
        mongo_backup_file = f'/tmp/mongo_logs_backup_{timestamp}.json'
        logging.info("Iniciando backup do MongoDB - Logs...")

        mongo_client = MongoClient('mongodb://mongo_user:mongo_password@mongodb:27017/')
        logs_db = mongo_client['logs']
        
        backup_data = {}
        collections = logs_db.list_collection_names()
        for collection_name in collections:
            collection = logs_db[collection_name]
            backup_data[collection_name] = list(collection.find({}))

        with open(mongo_backup_file, 'w') as f:
            json.dump(backup_data, f, default=str)
        
        logging.info("Backup do MongoDB - Logs concluído.")
        upload_to_minio(mongo_backup_file, f'backups/mongo/logs/{timestamp}.json')

    except Exception as e:
        logging.error(f"Erro ao fazer backup do MongoDB - Logs: {e}")

    if os.path.exists(mongo_backup_file):
        os.remove(mongo_backup_file)
        logging.info(f"Arquivo temporário {mongo_backup_file} removido.")


@shared_task
def backup_mongo_encrypt():
    timestamp = datetime.now().strftime('%Y%m%d%H%M%S')

    try:
        mongo_backup_file = f'/tmp/mongo_encrypt_backup_{timestamp}.json'
        logging.info("Iniciando backup do MongoDB - Encrypt...")

        mongo_client = MongoClient('mongodb://mongo_user:mongo_password@mongodb:27017/')
        encrypt_db = mongo_client['encrypt']
        
        backup_data = {}
        collections = encrypt_db.list_collection_names()
        for collection_name in collections:
            collection = encrypt_db[collection_name]
            backup_data[collection_name] = list(collection.find({}))

        with open(mongo_backup_file, 'w') as f:
            json.dump(backup_data, f, default=str)
        
        logging.info("Backup do MongoDB - Encrypt concluído.")
        upload_to_minio(mongo_backup_file, f'backups/mongo/encrypt/{timestamp}.json')

    except Exception as e:
        logging.error(f"Erro ao fazer backup do MongoDB - Encrypt: {e}")

    if os.path.exists(mongo_backup_file):
        os.remove(mongo_backup_file)
        logging.info(f"Arquivo temporário {mongo_backup_file} removido.")


def upload_to_minio(file_path, minio_path):
    try:
        with open(file_path, 'rb') as file_data:
            MINIO_CLIENT.put_object(
                'backups',
                minio_path,
                file_data,
                length=os.path.getsize(file_path),
            )
        logging.info(f"Backup enviado para o MinIO: {minio_path}")
    except Exception as e:
        logging.error(f"Falha ao enviar backup para o MinIO: {e}")
```
<p>
Neste projeto, utilizei o Celery para agendar e gerenciar tarefas assíncronas relacionadas à criação de backups do banco de dados PostgreSQL e MongoDB. Esses backups são armazenados em um servidor MinIO, que simula a funcionalidade do Amazon S3, garantindo uma solução eficiente e escalável para o armazenamento dos dados. As tarefas foram configuradas da seguinte forma:

Backup do PostgreSQL: A função backup_postgres realiza o backup das tabelas do banco PostgreSQL. A tarefa começa ao conectar-se ao banco de dados e copiar os dados de cada tabela para um arquivo SQL temporário. Depois, o arquivo gerado é enviado para o MinIO usando a função upload_to_minio, que é responsável por fazer o upload do arquivo para o MinIO. Após o upload, o arquivo temporário é removido. Caso ocorra algum erro durante o processo, ele é registrado nos logs.

Backup dos Logs do MongoDB: A função backup_mongo_logs faz o backup de dados do banco MongoDB da coleção de logs. O conteúdo de todas as coleções é recuperado e armazenado em um arquivo JSON temporário. Esse arquivo também é enviado para o MinIO, garantindo que os logs estejam preservados de forma segura. Como nas outras tarefas, em caso de erro, a falha é registrada e o arquivo temporário é excluído após o upload.

Backup de Dados Criptografados do MongoDB: A tarefa backup_mongo_encrypt é configurada de forma semelhante à anterior, mas neste caso, ela lida com dados da coleção "encrypt" do MongoDB. Os dados de todas as coleções dessa base são recuperados e armazenados em um arquivo JSON, que é enviado para o MinIO.

Função de Upload para o MinIO: A função upload_to_minio é responsável por enviar qualquer arquivo para o MinIO, garantindo que o backup seja armazenado no bucket correto. A função abre o arquivo em modo binário, obtém seu tamanho e faz o upload para o MinIO, gerenciando erros e registrando falhas nos logs.

Essas tarefas são agendadas para execução periódica com Celery e podem ser executadas independentemente, garantindo que os dados dos bancos PostgreSQL e MongoDB sejam mantidos de forma segura e eficaz. O uso do MinIO para armazenar os backups é uma estratégia que facilita a escalabilidade e a recuperação de dados em caso de falhas.

Essa abordagem não apenas automatiza o processo de backup, mas também proporciona uma camada adicional de segurança e confiabilidade no armazenamento dos dados essenciais para a operação do sistema.
</p>
</details>

---
## Contribuições Coletivas
### Aplicação Machine Learning
<details> <summary><b>Clique para ver o código e explicação</b></summary>

```python
import pandas as pd
from sklearn.preprocessing import scale, PowerTransformer
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score, davies_bouldin_score, calinski_harabasz_score


class RFMClient:
    def __init__(self, csv_path):
        self.csv_path = csv_path
        self.df = None
        self.df_rfm = None
        self.cluster_metrics_results = []

    def load_data(self):
        self.df = pd.read_csv(self.csv_path, encoding='latin1')
        self.df = self.df[self.df['deleted_at'].isnull()]
        self.df['created_at'] = pd.to_datetime(self.df['created_at'])
        self.df = self.df.query('value < 100000 & value > 0')

    def calculate_rfm(self):
        self.load_data()
        self.df_rfm = (
            self.df.groupby('participant_id')
            .agg(
                R=('created_at', lambda x: (pd.Timestamp.today() - x.max()).days),
                F=('asset_id', 'nunique'),
                M=('value', 'mean'),
            )
        )
        return self.df_rfm.reset_index().to_dict(orient='records')

    def preprocess_rfm(self):
        self.df_rfm = self.df_rfm.query('F < 100000 & M < 20000')
        scaler = PowerTransformer()
        self.df_rfm = pd.DataFrame(
            scaler.fit_transform(self.df_rfm), 
            index=self.df_rfm.index, 
            columns=self.df_rfm.columns
        )
        self.df_rfm = self.df_rfm.apply(lambda x: x.clip(upper=x.quantile(0.95)))
        return self.df_rfm.reset_index().to_dict(orient='records')

    def cluster_rfm(self, n_clusters=4):
        X = self.df_rfm.copy()
        kmeans = KMeans(n_clusters=n_clusters, random_state=0)
        self.df_rfm['Cluster'] = kmeans.fit_predict(X)
        return self.df_rfm.reset_index().to_dict(orient='records')

    def get_cluster_centers(self):
        """Retorna os centros dos clusters ajustados com as colunas apropriadas."""
        kmeans = KMeans(n_clusters=4, random_state=0)
        X = self.df_rfm.drop(columns=['Cluster'], errors='ignore')
        kmeans.fit(X)
        centers = pd.DataFrame(kmeans.cluster_centers_, columns=X.columns)
        centers.index = [f"Cluster {i+1}" for i in range(len(centers))]
        return centers.reset_index().to_dict(orient='records')

    def evaluate_clusters(self):
        X = self.df_rfm.drop(columns=['Cluster'], errors='ignore')
        for k in range(2, 11):
            model = KMeans(n_clusters=k, random_state=0)
            labels = model.fit_predict(X)
            cluster_results = {
                'k': k,
                'inertia': model.inertia_,
                'silhouette_score': silhouette_score(X, labels),
                'davies_bouldin_score': davies_bouldin_score(X, labels),
                'calinski_harabasz_score': calinski_harabasz_score(X, labels),
            }
            self.cluster_metrics_results.append(cluster_results)
        return self.cluster_metrics_results
```

O projeto desenvolvido consistiu na criação de uma aplicação utilizando Django como servidor Back-End para processar dados de machine learning. O sistema foi projetado para receber dados em formato CSV, calcular métricas de Recência, Frequência e Valor (RFM), e realizar a segmentação de clientes por meio de clustering utilizando KMeans.

Estrutura e Funcionalidade:
Leitura e Pré-processamento de Dados: A aplicação utiliza a biblioteca Pandas para carregar e filtrar os dados, removendo entradas desnecessárias e ajustando os valores de algumas colunas (como a transformação de created_at para tipo datetime).

Cálculo RFM: A classe RFMClient calcula três métricas chave para análise de comportamento de clientes:

- Recência (R): O número de dias desde a última compra do cliente.
- Frequência (F): O número de ativos únicos adquiridos por um cliente.
- Valor Monetário (M): O valor médio das transações feitas pelo cliente.
  
Essas métricas são calculadas para cada participant_id, gerando um DataFrame com as informações.
Pré-processamento dos Dados RFM: A classe aplica a transformação de dados com o PowerTransformer para normalizar as métricas e utiliza a função clip para remover outliers, garantindo que os dados sejam mais adequados para análise de clustering.

Clustering com KMeans: O modelo utiliza o KMeans para agrupar os clientes em clusters com base nas métricas RFM. O número de clusters pode ser ajustado, e a classificação dos clientes em clusters é retornada com o índice do cluster atribuído.

Avaliação dos Clusters: A aplicação avalia a qualidade dos clusters gerados, utilizando métricas como Silhouette Score, Davies-Bouldin Score, e Calinski-Harabasz Score. Essas métricas ajudam a determinar a qualidade do agrupamento e a adequação do número de clusters escolhido.

Implementação Django:
O Django foi utilizado para criar as rotas de API que recebem os dados e executam os cálculos necessários. O cliente, uma vez configurado, envia os dados via API para o servidor, que processa os dados, calcula as métricas RFM, realiza o clustering e retorna os resultados ao cliente.

Em resumo, a aplicação proporciona uma maneira eficiente de segmentar clientes e avaliar seu comportamento de compra, utilizando técnicas de machine learning em conjunto com uma arquitetura robusta para processamento e comunicação de dados.
</details>

---

## Tecnologias Utilizadas

- **Django (Backend)**: Framework robusto para o gerenciamento de dados, autenticação e segurança, que facilita a criação de APIs e a integração com banco de dados.
  
- **Python**: Linguagem principal usada para desenvolver a lógica de negócios e as APIs, bem como para integrar soluções de Machine Learning.

- **JavaScript**: Linguagem essencial para tornar a interface interativa, permitindo a comunicação entre o Front-End e o Back-End.

- **Vue.js (Frontend)**: Framework JavaScript utilizado para criar interfaces de usuário dinâmicas, interativas e responsivas.

- **PostgreSQL**: Banco de dados relacional utilizado para armazenar dados principais do sistema, como informações de usuários e dados operacionais.

- **MongoDB**: Banco de dados NoSQL utilizado para armazenar logs e chaves de usuário, oferecendo flexibilidade para dados não estruturados.

- **FastAPI**: Framework eficiente para a criação de APIs rápidas e de alto desempenho, especialmente utilizado para integrar e servir modelos de Machine Learning.

---

## Conclusão

Esse projeto me proporcionou uma experiência completa no desenvolvimento de sistemas com integração entre **Back-End** e **Front-End**, além de me permitir aprender como trabalhar com diferentes bancos de dados e integrar modelos de **Machine Learning** em aplicações reais. 
Aprendi a lidar com dados em grande escala, realizar transformações, e aplicar técnicas de clustering para segmentação de clientes, aprimorando tanto minhas habilidades técnicas quanto de resolução de problemas. Esse conhecimento será fundamental para projetos futuros, especialmente ao integrar mais tecnologias e otimizar a performance do sistema.
