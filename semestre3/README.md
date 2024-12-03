### Sistema de Predição de Vendas - Dom Rock
3° Semestre - 01/2023

Parceiro Acadêmico: Dom Rock
<p align="center"><img src="https://github.com/Ariane-Sousa/bertoti/assets/108765052/bbd9f4c7-56bf-4563-9da0-16977ffb6ac8" widht="20%"></img>

---

## Empresa parceira

A Dom Rock é uma empresa que oferece soluções utilizando tecnologia de dados para ampliar resultados em marketing, vendas, distribuição, logística, operações, engenharia e finanças.
Utilizando modelos matemáticos e algoritmos baseados em aprendizado de máquina que endereçam duas soluções sendo Nxt.Demand com quatro produtos – Vox, Sales&Distribution, Marketing&Planning, Pricing – e Nxt.Operations com dois produtos – Matching&Risk e Optimization.

---

## 💻 Nossa proposta

A empresa Dom Rock enfrentava a tarefa de padronizar os arquivos de predição de vendas de seus clientes, fornecidos no formato CSV. Reconhecendo a necessidade de otimizar esse processo, a empresa buscava desenvolver uma aplicação web que facilitasse a inserção e padronização desses dados, resultando em uma redução significativa do tempo dedicado a essa tarefa.

Neste semestre, o nosso grupo está propondo uma solução abrangente para a empresa. O desafio central envolve lidar de maneira eficaz com o histórico de movimentação de produtos, englobando tanto as informações de vendas quanto de estoque. Além disso, a solução visa integrar a predição de faturamento, realizada por um algoritmo de inteligência artificial já existente. Complementarmente, a aplicação será capaz de incorporar os dados provenientes da equipe de vendas, relacionados ao planejamento futuro da empresa.

Diante dessa complexidade, nossa proposta visa criar uma plataforma que harmonize e simplifique esses processos, proporcionando à Dom Rock uma gestão mais eficiente e informada de suas operações comerciais.

---

## Jornada do usuário 

<h3 align="center">Administrador</h3>
<p align="center"><img src="https://github.com/Ariane-Sousa/bertoti/assets/108765052/9531f904-1ece-4ff3-901a-6a47299b344b" widht="20%"></img>

<h3 align="center"> Vendedor </h3>
<p align="center"><img src="https://github.com/Ariane-Sousa/bertoti/assets/108765052/0e703c34-f28e-45df-94eb-c607575095e5" widht="20%"></img>

---

## Modelagem

<h3 align="center">Modelagem Lógico</h3>
<p align="center"><img src="https://github.com/Ariane-Sousa/bertoti/assets/108765052/a498c64f-808e-421b-8f27-548bb546585f" widht="20%"></img>

---


## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

- **Desenvolvimento Front-End com JavaScript**: Aprofundei meus conhecimentos em JavaScript, criando interfaces interativas e dinâmicas para o usuário.
  
- **Banco de Dados com PostgreSQL**: Utilizei o PostgreSQL como banco de dados para armazenar e manipular grandes volumes de informações de forma segura e eficiente. Aprendi a escrever consultas, otimizar a performance do banco e garantir a integridade dos dados.
  
- **Integração Front-End e Back-End**: Aprimorei a comunicação entre o front-end e o back-end, utilizando APIs RESTful para garantir uma integração fluída entre a interface do usuário e os dados armazenados no servidor.
  
- **Controle de Versão com Git**: Utilizei Git para controle de versão, garantindo que o código fosse mantido de forma organizada e que as mudanças fossem registradas adequadamente durante o desenvolvimento.
  
---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

- **Inteligência Emocional**: Trabalhei no desenvolvimento da minha inteligência emocional para lidar com situações de pressão, estresse e desafios do projeto de forma equilibrada, mantendo uma atitude positiva e focada.
  
- **Capacidade de Delegação**: Aprendi a identificar as habilidades e forças de cada membro da equipe e delegar responsabilidades de acordo com essas competências, otimizando o desempenho do grupo.
  
- **Gestão de Expectativas**: Desenvolvi a habilidade de gerenciar as expectativas de stakeholders e membros da equipe, garantindo que os objetivos do projeto estivessem alinhados com as capacidades do time e os prazos estabelecidos.
  
- **Resiliência**: Enfrentei diversos obstáculos e contratempos ao longo do projeto, mas com resiliência, mantive o foco nos objetivos e busquei soluções para superar as dificuldades, aprendendo com os erros ao longo do caminho.

---

## Contribuições Individuais
<details>
  <summary><b>Front-End: Personalização e criação de gráficos</b></summary>
  <br>
  <p>Desenvolvi funções geradoras de gráficos no Front-end do nosso projeto que realizam uma consulta no nosso banco de dados, buscando informações dos vendedores, suas vendas e metas. De acordo com esses dados, eram gerados gráficos, o exemplo que trouxe abaixo, gerou um gráfico dos dez melhores vendedores, comparando por metas, e dos dez produtos mais vendidos. 
  </p>
  
  ```javascript
  
function generateVendedoresChart() {
  fetch("http://localhost:8080/venda/topVendedores")
    .then(function (response) {
      return response.json();
    })
    .then(function (data) {
      var dados = data.map(function (item) {
        return { y: item.nome_usuario, a: item.total_vendido, nome: item.nome_completo };
      });

      var config = {
        data: dados,
        xkey: "y",
        ykeys: "a",
        labels: ["Total"],
        fillOpacity: 0.6,
        hideHover: "auto",
        behaveLikeLine: true,
        resize: true,
        pointFillColors: ["#ffffff"],
        pointStrokeColors: ["black"],
        lineColors: ["#005eff"],
        xLabelAngle: 45,
      };

      config.element = "stackedVendedores";
      config.stacked = true;
      Morris.Bar(config);
    })
    .catch(function (error) {
      console.log(error);
    });
}


function generateProdutosChart() {
  fetch("http://localhost:8080/produto/topProdutos")
    .then(function (response) {
      return response.json();
    })
    .then(function (data) {
      var dados = data.map(function (item) {
        return { y: item.nome_produto, a: item.total_vendido };
      });

      var config = {
        data: dados,
        xkey: "y",
        ykeys: "a",
        labels: ["Total"],
        fillOpacity: 0.6,
        hideHover: "auto",
        behaveLikeLine: true,
        resize: true,
        pointFillColors: ["#ffffff"],
        pointStrokeColors: ["black"],
        lineColors: ["#005eff"],
        xLabelAngle: 45,
      };

      config.element = "stackedProdutos";
      config.stacked = true;
      Morris.Bar(config);
    })
    .catch(function (error) {
      console.log(error);
    });
}
  
  ```
  ![Dados-ADMIN](https://github.com/Ariane-Sousa/bertoti/assets/108765052/ed7fd5fe-27ad-48f9-afc8-6d3db8f6c5ce)

  <p><i>No código fornecido, há duas funções, generateVendedoresChart e generateProdutosChart, que utilizam a função fetch para realizar requisições a endpoints locais (topVendedores e topProdutos). Esses endpoints retornam dados sobre os principais vendedores e produtos, respectivamente. Após receber a resposta em formato JSON, os dados são mapeados e transformados para um formato adequado para a biblioteca Morris.js, que é utilizada para gerar gráficos de barras empilhadas. Os gráficos resultantes são exibidos em elementos HTML específicos, como "stackedVendedores" e "stackedProdutos". Em caso de erro durante as requisições, os detalhes são registrados no console.</i></p>
  <br>
</details>
<details>
  <summary><b>Back-end: Personalização e criação de endpoints</b></summary>
  <br>
  <p>Dsenvolvi endpoints que realizam uma consulta no nosso banco de dados, buscando informações dos vendedores, suas vendas e metas. De acordo com esses dados, meus endpoints me retornavam as informações dos vendedores que mais atingiram as metas, e dos produtos que foram mais vendidos.</p>
  
  ```java
  
  @CrossOrigin(origins = "*", allowedHeaders = "*")
    @GetMapping("/acima-meta")
    public ResponseEntity<?> getVendedoresAcimaMeta() {
        List<Venda> vendedoresAcimaMeta = repository.findVendedoresAcimaMeta();
        return ResponseEntity.ok(vendedoresAcimaMeta);
    }

  ```

 
  ```java
  
  @CrossOrigin(origins = "*", allowedHeaders = "*")
    @GetMapping("/topProdutos")
    public List<Map<String, Object>> getTopProdutos() {
        List<Map<String, Object>> topProdutos = new ArrayList<>();
        String sql = "SELECT p.nome_produto, " +
                "SUM(v.quant_vendida) AS total_vendido " +
                "FROM produto p " +
                "JOIN venda v ON p.cod_produto = v.fk_produto_cod_produto " +
                "GROUP BY p.nome_produto, v.fk_produto_cod_produto " +
                "ORDER BY total_vendido DESC " +
                "LIMIT 10";
        List<Map<String, Object>> rows = jdbcTemplate.queryForList(sql);
        for (Map<String, Object> row : rows) {
            Map<String, Object> produto = new HashMap<>();
            produto.put("nome_produto", ((String) row.get("nome_produto")).trim());
            produto.put("total_vendido", row.get("total_vendido"));
            topProdutos.add(produto);
        }
        return topProdutos;
    }

  ```
  
  <p><i>No primeiro trecho de código em Java, é definido um controlador de endpoint com a anotação @GetMapping("/acima-meta"). Este endpoint, ao ser acessado, retorna uma resposta HTTP contendo uma lista de vendedores que estão acima da meta de vendas. Esses dados são obtidos através da chamada do método findVendedoresAcimaMeta no repositório associado. A resposta é encapsulada em um objeto ResponseEntity e retorna um status HTTP 200 (OK) juntamente com a lista de vendedores ou um status de erro caso ocorra alguma exceção.
No segundo trecho de código, também em Java, é definido outro controlador de endpoint com a anotação @GetMapping("/topProdutos"). Esse endpoint realiza uma consulta SQL utilizando o JdbcTemplate para obter os top 10 produtos com base na quantidade total vendida. A resposta é uma lista de mapas, onde cada mapa contém informações sobre um produto, incluindo o nome do produto e a quantidade total vendida. Esses dados são processados e formatados antes de serem retornados como resultado do endpoint. A anotação @CrossOrigin permite solicitações de qualquer origem, facilitando a integração com front-ends em diferentes domínios.</i></p>
  <br>
</details>
<details>
  <summary><b>Refatoramento de todas as nossas páginas</b></summary>
  <br>
  <p>Implementei uma mudança de estilos, conversado e avaliado pelo grupo, na última sprint, todas as páginas passaram por refatoramento de CSS.</p>
</details>

---

## Contribuições Coletivas
### Tela de Cadastro de Clientes
<details> <summary><b>Clique para ver o código e explicação</b></summary>

```javascript
const formulario = document.querySelector("form");
const Inome_cliente = document.getElementById("nome_cliente");
const Inome_gerencia = document.getElementById("nome_gerencia");
const select = document.getElementById('caixa-de-selecao');
let list = [];
function cadastrar() {
    const nomeVendedor = select.value.toString();
    fetch(`http://localhost:8080/usuario/usuario-por-nome?nome=${nomeVendedor}`)
      .then(response => response.json())
      .then(data => {
        const idVendedor = parseInt(data);
        console.log(idVendedor);
        list.push(idVendedor); 
        const primeiroValor = list[0];
        const id = parseInt(primeiroValor);
        console.log(id);
        fetch("http://localhost:8080/cliente", {
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          method: "POST",
          body: JSON.stringify({
            nome_cliente: Inome_cliente.value,
            nome_gerencia: Inome_gerencia.value,
            fk_usuario_id: id
          })
        })
      })
      .catch(error => {
        console.error(error);
        alert("Erro ao buscar vendedor.");
      });
  };
function limpar(){
    Inome_cliente.value = "";
    Inome_gerencia.value = "";
}
formulario.addEventListener('submit', function(event){
    event.preventDefault();
    if (Inome_cliente.value === "" || Inome_cliente.value === "" ) {
        alert("Insira todos os campos.");
    } else {
        cadastrar();
        alert("Cliente cadastrado com sucesso.");
    }
});
fetch("http://localhost:8080/usuario")
    .then(response => response.json())
    .then(data => {
        data.forEach(usuario => {
            const option = document.createElement('option');
            option.text = usuario.nome;
            select.appendChild(option);
        });
    })
    .catch(error => console.error(error));
```

Participei da criação do frontend dessa tela, focando tanto na estilização quanto na implementação dos serviços de backend. A interação com o backend foi feita por meio de requisições fetch para obter e enviar dados. O formulário permite cadastrar um cliente, associando-o a um vendedor selecionado de uma lista populada dinamicamente a partir do backend. Além disso, implementei a lógica de validação de campos, garantindo que todos os dados fossem preenchidos antes do envio, e a funcionalidade de limpeza dos campos após o cadastro. A integração entre o frontend e o backend foi fundamental para o sucesso dessa funcionalidade.
</details>


---

## Tecnologias Utilizadas

- **JavaScript**: Utilizado para desenvolver a interface interativa da aplicação, proporcionando uma experiência de usuário dinâmica e responsiva. Ferramentas como React ou Vue.js (dependendo da escolha) foram essenciais para a construção de componentes reutilizáveis e eficientes.

- **Java**: A escolha do Java para o desenvolvimento do backend permitiu a criação de uma aplicação robusta e escalável, utilizando frameworks como Spring Boot para facilitar a criação de APIs RESTful e integração com o banco de dados.

- **PostgreSQL**: Utilizado para armazenar e gerenciar os dados da aplicação de forma eficiente, garantindo a integridade e segurança das informações. A escolha do PostgreSQL foi ideal para lidar com dados estruturados e realizar consultas complexas.


## Conclusão
Este projeto foi uma oportunidade valiosa para aprimorar minhas habilidades tanto técnicas quanto interpessoais. Aprendi a integrar diferentes tecnologias, como JavaScript, Java e PostgreSQL, para construir uma aplicação funcional e escalável. Além disso, desenvolvi uma compreensão mais profunda sobre a importância da comunicação e colaboração em equipe, e como gerenciar o tempo e os recursos para cumprir prazos e metas. Enfrentei desafios técnicos que me ajudaram a melhorar minha capacidade de resolução de problemas, e a experiência foi fundamental para meu crescimento como desenvolvedor.
