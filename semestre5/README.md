### Sistema de Processamento de Contas - Tecsus
5° Semestre - 01/2024

Parceiro Acadêmico: Tecsus

## 💻 Nossa proposta

A TecSUS atua na coleta e processamento de contas de energia, água e gás para empresas de diversos setores, incluindo atacado e varejo. O trabalho envolve a captura detalhada de cada campo das contas, garantindo que todas as informações sejam armazenadas em um banco de dados, facilitando consultas futuras e análises tanto técnicas quanto financeiras. Essas análises podem gerar insights valiosos para os clientes, como oportunidades de redução de custos e ajustes nos contratos.

Cada unidade de um cliente pode ter múltiplos contratos — seja de água, energia ou gás — e cada contrato pode gerar várias contas (ou faturas) mensalmente. Esses contratos estão vinculados a concessionárias específicas, responsáveis pelo fornecimento dos serviços.

Atualmente, a TecSUS conta com um banco de dados desestruturado, em formato de arquivo texto, contendo informações sobre unidades, contratos, contas e concessionárias. O objetivo da empresa é implementar técnicas de ETL (Extração, Transformação e Carregamento) para organizar esses dados, além de explorar ferramentas de visualização que proporcionem uma visão clara e estratégica das informações, aprimorando a gestão e as oportunidades de otimização para os clientes.

---

## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

- **Desenvolvimento Web**: Aprofundei meus conhecimentos em HTML, CSS e JavaScript, criando uma interface responsiva e intuitiva para oferecer uma experiência de usuário agradável.

- **Vue.js**: Desenvolvi componentes dinâmicos e interativos com Vue.js, aperfeiçoando habilidades em criação de interfaces modernas, responsivas e reativas.

- **Django**: Estruturei o Back-End com Django, implementando autenticação e segurança para garantir o gerenciamento seguro de dados, além de construir APIs RESTful que permitem integração eficiente com o Front-End.

- **Python**: Utilizei Python para manipular dados e estruturar toda a lógica de negócios, aumentando a produtividade e garantindo um código eficiente e bem-organizado.

---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

- **Trabalho em Equipe**: Colaborei de forma eficaz com a equipe, definindo requisitos, priorizando tarefas e alinhando prazos, desenvolvendo habilidades de comunicação e cooperação para alcançar objetivos compartilhados.

- **Resolução de Problemas**: Enfrentei e solucionei desafios técnicos durante o desenvolvimento, buscando soluções inovadoras para problemas complexos e aprimorando minha capacidade de adaptação em situações críticas.

- **Gerenciamento de Tempo**: Organizei meu tempo de forma eficiente, equilibrando as demandas do projeto com outras responsabilidades, o que me permitiu cumprir prazos e manter a qualidade em todas as entregas.

- **Aprendizado Contínuo**: Investi em desenvolver novas habilidades e expandir meus conhecimentos, sempre em busca de aprimoramento técnico e pessoal para melhorar minha performance e agregar valor aos projetos.

- **Adaptabilidade**: Mantive a flexibilidade em meio a mudanças e novos desafios, ajustando estratégias rapidamente e garantindo o andamento dos projetos com foco em resultados e soluções.

- **Comunicação Eficaz**: Apliquei uma comunicação clara e objetiva para manter a equipe alinhada, compartilhar avanços e apresentar resultados, promovendo um ambiente de colaboração e confiança.

- **Proatividade**: Tomei iniciativa em situações desafiadoras, identificando oportunidades de melhoria no projeto e contribuindo para decisões estratégicas que beneficiaram o desenvolvimento do software.

---

## Contribuições Individuais
<details>
<summary><b>Upload de Arquivos</b></summary>
<br>
<p></p>
  
```python

class InserirDadosAPIView(APIView):
    def post(self, request):
        tipo_documento = request.data.get('tipo_documento')
        arquivo_csv = request.FILES.get('arquivo_csv')

        if not tipo_documento or not arquivo_csv:
            return Response({'error': 'Tipo de documento e arquivo CSV são necessários.'}, status=status.HTTP_400_BAD_REQUEST)

        try:
            pasta_csv = 'csv_upload/agua'
            caminho_csv = os.path.join(pasta_csv, arquivo_csv.name)
            caminho_relatorio = default_storage.save(caminho_csv, arquivo_csv)            
            if tipo_documento == 'contrato':
                self.inserir_contratos_do_csv(caminho_csv)
            elif tipo_documento == 'fatura':
                self.inserir_faturas_do_csv(caminho_csv)
            else:
                return Response({'error': 'Tipo de documento inválido.'}, status=status.HTTP_400_BAD_REQUEST)
            return Response({'success': f'Dados do {tipo_documento} inseridos com sucesso.'}, status=status.HTTP_201_CREATED)
        except Exception as e:
            return Response({'error': str(e)}, status=status.HTTP_500_INTERNAL_SERVER_ERROR)

    def inserir_contratos_do_csv(self, caminho_do_csv):
        with default_storage.open(caminho_do_csv, 'r') as arquivo_csv:
            leitor_csv = csv.DictReader(arquivo_csv)
            for linha in leitor_csv:
                numero_cliente = linha['Número Cliente'] or None
                
                numero_contrato = linha['Número Contrato']
                if not numero_contrato.isdigit():
                    numero_contrato = None

                codigo_de_ligacao_rgi = linha['Código de Ligação (RGI)']
                if ClienteContrato.objects.filter(codigo_de_ligacao_rgi=codigo_de_ligacao_rgi).exists():
                    continue

                fornecedor_agua, _ = FornecedorAgua.objects.get_or_create(
                    fornecedor=linha['Fornecedor'],
                    cod_companhia=linha['Codificação da Companhia'],
                    planta=linha['Planta'],
                    codigo_de_ligacao_rgi=codigo_de_ligacao_rgi
                )

                endereco, _ = Endereco.objects.get_or_create(
                    endereco_instalacao=linha['Endereço de Instalação'],
                    cidade=linha['Nome do Contrato'],
                    codigo_de_ligacao_rgi=codigo_de_ligacao_rgi
                )

                contrato, _ = ClienteContrato.objects.get_or_create(
                    nome_contrato=linha['Nome do Contrato'],
                    email=linha['Campo Extra de Acesso 1'],
                    ativo=linha['Ativado'],
                    numero_contrato=numero_contrato,
                    numero_cliente=numero_cliente,
                    codigo_de_ligacao_rgi=codigo_de_ligacao_rgi
                )

    def inserir_faturas_do_csv(self, caminho_do_csv):
        with default_storage.open(caminho_do_csv, 'r') as arquivo_csv:
            leitor_csv = csv.DictReader(arquivo_csv)
            for linha in leitor_csv:
                contrato = ClienteContrato.objects.get(codigo_de_ligacao_rgi=linha['Código de Ligação (RGI)'])

                endereco_instalacao = linha.get('Endereço de Instalação', 'Endereço desconhecido')

                cidade = linha.get('Cidade', '')

                endereco, _ = Endereco.objects.get_or_create(
                    endereco_instalacao=endereco_instalacao,
                    cidade=cidade
                )

                consumo_agua_m3 = self.converter_para_decimal(linha['Consumo de Água m³'])
                consumo_esgoto_m3 = self.converter_para_decimal(linha['Consumo de Esgoto m³'])
                vlr_agua = self.converter_para_decimal(linha['Valor Água R$'])
                vlr_esgoto = self.converter_para_decimal(linha['Valor Esgoto R$'])
                vlr_total = self.converter_para_decimal(linha['Total R$'])

                leitura_anterior = self.converter_para_data(linha['Leitura Anterior'])
                leitura_atual = self.converter_para_data(linha['Leitura Atual'])

                FatoContratoAgua.objects.create(
                    codigo_de_ligacao_rgi=contrato,
                    id_endereco=endereco,
                    consumo_agua_m3=consumo_agua_m3,
                    consumo_esgoto_m3=consumo_esgoto_m3,
                    vlr_agua=vlr_agua,
                    vlr_esgoto=vlr_esgoto,
                    vlr_total=vlr_total,
                    leitura_anterior=leitura_anterior,
                    leitura_atual=leitura_atual,
                )

    def converter_para_decimal(self, valor_str):
            valor_str = valor_str.strip().replace('.', '').replace(',', '.')
            return float(valor_str)
    
    def converter_para_data(self, data_str):
        try:
            if data_str == '00/00/0000':
                return None
            else:
                return datetime.strptime(data_str, '%d/%m/%Y')
        except ValueError:
            return None
```
<p>Essa API permite a inserção de dados de contratos e faturas a partir de arquivos CSV. O endpoint verifica o tipo de documento e o arquivo enviado pelo usuário, salvando o arquivo em uma pasta específica. Dependendo do tipo de documento (contrato ou fatura), o método correspondente (inserir_contratos_do_csv ou inserir_faturas_do_csv) é chamado para processar o CSV, extraindo e armazenando os dados no banco de dados.

Para contratos, são verificados e criados registros de fornecedores e endereços, e para faturas, são registrados detalhes de consumo e valores. Funções auxiliares convertem strings em valores decimais e datas para garantir consistência ao salvar as informações.</p>
</details>

<details>
<summary><b>Relatório Mensal de Energia</b></summary>
<br>
<p>O código abaixo implementa o controlador de autenticação (AuthController), responsável por lidar com as solicitações de autenticação dos usuários. Aqui está uma explicação detalhada do que acontece no código:</p>

```python
from datetime import datetime, timedelta
from django.db.models import Avg
from .models import FatoContratoAgua

def calcular_media_ultimos_tres_meses(cod_ligacao_rgi):
    hoje = datetime.now()
    tres_meses_atras = hoje - timedelta(days=90)
    tres_meses_atras = datetime(tres_meses_atras.year, tres_meses_atras.month, 1)

    media_ultimos_tres_meses = FatoContratoAgua.objects.filter(
        codigo_de_ligacao_rgi=cod_ligacao_rgi,
        leitura_atual__gte=tres_meses_atras,
        leitura_atual__lt=hoje
    ).aggregate(Avg('vlr_total'))

    return media_ultimos_tres_meses['vlr_total__avg'] or 0

def calcular_media_mes_atual(cod_ligacao_rgi):
    hoje = datetime.now()
    primeiro_dia_do_mes = datetime(hoje.year, hoje.month, 1)
    proximo_mes = hoje.month % 12 + 1
    proximo_ano = hoje.year + (hoje.month // 12)
    primeiro_dia_proximo_mes = datetime(proximo_ano, proximo_mes, 1)
    
    media_mes_atual = FatoContratoAgua.objects.filter(
        codigo_de_ligacao_rgi=cod_ligacao_rgi,
        leitura_atual__gte=primeiro_dia_do_mes,
        leitura_atual__lt=primeiro_dia_proximo_mes
    ).aggregate(Avg('vlr_total'))

    return media_mes_atual['vlr_total__avg'] or 0

def comparar_media_mes_atual_com_ultimos_tres_meses(cod_ligacao_rgi):
    media_ultimos_tres_meses = calcular_media_ultimos_tres_meses(cod_ligacao_rgi)
    media_mes_atual = calcular_media_mes_atual(cod_ligacao_rgi)

    if media_mes_atual > media_ultimos_tres_meses:
        return "O valor médio deste mês é maior que a média dos últimos três meses."
    elif media_mes_atual < media_ultimos_tres_meses:
        return "O valor médio deste mês é menor que a média dos últimos três meses."
    else:
        return "O valor médio deste mês é igual à média dos últimos três meses."
```
<p>Este conjunto de funções calcula e compara médias de valores mensais para um contrato específico, e esses cálculos são usados para enviar e-mails informativos aos usuários.

calcular_media_ultimos_tres_meses(cod_ligacao_rgi): Esta função calcula a média dos valores de contas (vlr_total) dos últimos três meses para um contrato identificado pelo código de ligação cod_ligacao_rgi. Para isso, ela filtra os registros com data de leitura atual dentro desse período e retorna a média dos valores encontrados.

calcular_media_mes_atual(cod_ligacao_rgi): Esta função calcula a média do valor total (vlr_total) do mês atual para o mesmo contrato, considerando apenas as leituras dentro do intervalo do primeiro dia do mês até o início do mês seguinte.

comparar_media_mes_atual_com_ultimos_tres_meses(cod_ligacao_rgi): Esta função compara a média do mês atual com a média dos últimos três meses. Dependendo do resultado da comparação, ela retorna uma mensagem indicando se o valor médio atual é maior, menor ou igual à média dos três meses anteriores.

Esses cálculos permitem à aplicação identificar variações nos custos e enviar notificações aos usuários por e-mail, oferecendo informações sobre o comportamento do consumo e ajudando a monitorar potenciais aumentos ou reduções nos valores médios.
</p>
</details>


<details>
<summary><b>Testes unitários</b></summary>

```javascript
import { mount } from '@vue/test-utils';
import Upload from '@/views/Upload.vue';

describe('Upload', () => {
  
  it('renderiza corretamente', () => {
    const wrapper = mount(Upload);
    expect(wrapper.exists()).toBe(true);
  });

  it('clears data when clearData method is called', async () => {
    const wrapper = mount(Upload);
    
    wrapper.vm.fileInputValue = 'fake file';
    wrapper.vm.countTypeValue = 'agua';
    wrapper.vm.documentTypeValue = 'contrato';

    await wrapper.vm.clearData();

    // Verificação da função de limpar dados
    expect(wrapper.vm.fileInputValue).toBe(null);
    expect(wrapper.vm.countTypeValue).toBe(null);
    expect(wrapper.vm.documentTypeValue).toBe(null);
  });

});
```
## **Resumo sobre os Testes Unitários Implementados**

Implementei testes unitários no sistema para garantir a funcionalidade e confiabilidade do código. Como parte dessa melhoria, o repositório agora está protegido por um **hook de commit**, que impede que commits sejam realizados caso algum teste unitário falhe. Isso assegura que apenas código validado seja integrado ao projeto.

### **Descrição dos Testes Implementados**

#### **Componente Upload**
O componente `Upload.vue` foi testado para validar seu comportamento esperado:

1. **Renderização do Componente**
   - O teste verifica se o componente é renderizado corretamente ao ser montado.  
   - Resultado esperado: O componente deve existir na árvore DOM.

2. **Limpeza de Dados**
   - O método `clearData` do componente foi testado para garantir que ele redefine os valores de entrada corretamente.  
   - Resultado esperado: Após a execução do método, os valores de `fileInputValue`, `countTypeValue`, e `documentTypeValue` devem ser `null`.

### **Impacto**
Com a implementação dos testes e a configuração do **hook de commit**, o fluxo de desenvolvimento foi aprimorado. Esse mecanismo:
- Eleva a qualidade do código ao prevenir a inclusão de alterações com falhas.
- Oferece maior segurança para a equipe de desenvolvimento, reduzindo o risco de regressões.
</details>

## Contribuições Coletivas
### Modelagem
<details> <summary><b>Clique para ver o código e explicação</b></summary>

```python
from django.db import models


class FornecedorAgua(models.Model):
    id_fornecedor_agua = models.AutoField(primary_key=True)
    fornecedor = models.CharField(max_length=255)
    cod_companhia = models.CharField(max_length=255)
    planta = models.CharField(max_length=255)
    codigo_de_ligacao_rgi = models.CharField(max_length=255, unique=True)


class Endereco(models.Model):
    id_endereco = models.AutoField(primary_key=True)
    endereco_instalacao = models.CharField(max_length=255)
    cidade = models.CharField(max_length=255)
    codigo_de_ligacao_rgi = models.CharField(max_length=255, null=True)


class ClienteContrato(models.Model):
    nome_contrato = models.CharField(max_length=255, null=True)
    email = models.EmailField()
    ativo = models.CharField(max_length=255)
    numero_contrato = models.BigIntegerField(null=True)
    numero_cliente = models.BigIntegerField(null=True)
    codigo_de_ligacao_rgi = models.CharField(max_length=255, primary_key=True)


class FatoContratoAgua(models.Model):
    id_contrato_agua = models.AutoField(primary_key=True)
    codigo_de_ligacao_rgi = models.ForeignKey(ClienteContrato, on_delete=models.CASCADE)
    id_endereco = models.ForeignKey(Endereco, on_delete=models.CASCADE)
    consumo_agua_m3 = models.DecimalField(max_digits=1000, decimal_places=2)
    consumo_esgoto_m3 = models.DecimalField(max_digits=1000, decimal_places=2)
    vlr_agua = models.DecimalField(max_digits=1000, decimal_places=2)
    vlr_esgoto = models.DecimalField(max_digits=1000, decimal_places=2)
    vlr_total = models.DecimalField(max_digits=1000, decimal_places=2)
    leitura_anterior = models.DateField(null=True)
    leitura_atual = models.DateField(null=True)
```
Contribuí para a modelagem do sistema utilizando o **formato estrela**, que organiza os dados em torno de uma tabela principal (fato) conectada a tabelas de dimensão. Essa estrutura é amplamente utilizada em **data warehouses** para facilitar análises e relatórios.

</details>

---

## Tecnologias Utilizadas

- **Django**: Framework web que fornece uma estrutura robusta para o desenvolvimento do Back-End, incluindo gerenciamento de dados, autenticação e segurança.

- **Python**: Linguagem de programação usada para implementar toda a lógica de negócios e as APIs no Back-End com Django.

- **JavaScript**: Linguagem utilizada para adicionar interatividade à interface da aplicação e gerenciar a comunicação entre o Back-End e o Front-End.

- **Vue.js**: Framework JavaScript responsável pela construção da interface do usuário, garantindo uma experiência ágil, responsiva e interativa.

- **PostgreSQL**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações de usuários, autenticação e dados operacionais da aplicação.



---

## Conclusão
Durante o desenvolvimento deste projeto, aprofundei meus conhecimentos em tecnologias essenciais como Django e Vue.js, aprendendo a construir uma arquitetura robusta e eficiente. O domínio de Python e JavaScript foi consolidado com a criação de lógicas de negócios e interatividade no Front-End. 

Além disso, o uso de Oracle SQL me permitiu compreender a importância de uma modelagem de dados bem estruturada para atender às demandas de um sistema real. Esses aprendizados foram fundamentais para meu crescimento técnico e profissional.
