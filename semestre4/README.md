### Jaia
4° Semestre - 02/2023

Parceiro Acadêmico: Jaia

## 💻 Nossa proposta

Jaia Software Em um cenário onde a paisagem urbana se compõe de uma mistura de edifícios modernos e históricos, a empresa Jaia, apresentou um desafio significativo. A condução de inspeções prediais estava provando ser uma tarefa morosa e suscetível a imprecisões. Diante desse cenário, a Jaia buscou soluções inovadoras para otimizar esse processo crucial. A visão estratégica da empresa contemplou o desenvolvimento de um software de inspeção predial, projetado para revolucionar a abordagem atual. A plataforma concebida promete oferecer uma experiência intuitiva, capacitando os inspetores a documentar minuciosamente detalhes relevantes e capturar evidências visuais de forma eficaz. Adicionalmente, a geração instantânea de relatórios abastecerá a tomada de decisões embasadas. A Jaia, reconhecendo a necessidade de aprimorar a qualidade e eficiência das inspeções, direcionou seus esforços para o desenvolvimento desse software inovador. O resultado obtido transcendeu as expectativas iniciais, beneficiando não somente a empresa, mas também elevando o padrão das inspeções prediais na esfera urbana, contribuindo, assim, para uma maior segurança e excelência nas estruturas urbanas.

## Modelagem do Banco

### <p align="center">DER</p>
<p align="center"><img src="./model-der.png" widht="20%"></img>

### <p align="center">Mer</p>
<p align="center"><img src="./model-mer.png" widht="20%"></img>

## Contribuições Individuais
<details>
<summary><b>Landing Page: Introdução ao Projeto</b></summary>
<br>
<p>O código acima implementa a página inicial (landing page) do projeto, fornecendo uma introdução ao projeto, exibindo suas principais soluções e facilitando o contato com a empresa através do botão "Fale Conosco".</p>
  
```javascript
<template>
    <div class="landing-page" id="landingPage">
        <section id="home">
            <div class="wrapper">
                <div class="home-titulo">
                    <h2 class="title">O que é a Predial?</h2>
                    <p class="tittle-somos">
                        A Predial é a sua solução confiável para inspeções prediais sob medida. Somos uma plataforma dedicada a atender às necessidades dos nossos clientes que buscam inspecionar seus edifícios com eficiência e precisão.
                        <br />
                        <br />
                        Concebida pela Jaia, a Predial permite que proprietários de edifícios, gerentes e administradores solicitem inspeções personalizadas para seus imóveis. Nossa plataforma intuitiva facilita o processo de agendar e coordenar inspeções, além de oferecer uma maneira eficaz de documentar detalhes relevantes e capturar evidências visuais.
                        <br />
                        <br />
                        Com a Predial, você pode contar com relatórios instantâneos que embasam decisões fundamentadas. Elevamos o padrão das inspeções prediais, contribuindo para uma maior segurança e excelência nas estruturas urbanas. Confie na Predial para cuidar das suas necessidades de inspeção predial de forma eficiente e confiável.
                    </p>
                    <a href="https://wa.me/5512982156294" target="_blank">
                        <button class="button">
                        <img src="@/assets/whats.png" alt="Logo" class="whats-logo" />
                        Fale Conosco
                        </button>
                    </a>
                </div>
                <div class="home-img">
                <img class="celular" src="@/assets/celular.png" alt="Celular com logo">
                </div>
            </div>  
        </section>
        <div class="solucoes" id="solucoes">
            <p class="title">Soluções</p>
            <div class="container">   
                <div class="ordem-servico box">
                    <img src="@/assets/solucoes1.png" alt="Ordem de Serviço"/>
                    <h>Ordem de Serviço</h>
                    <span class="button-solucoes" id="detalhes-os" @click="detalhesOS = true">Ver detalhes</span>
                    <v-dialog v-model="detalhesOS" width="80%">
                            <OrdemServicoForm></OrdemServicoForm>
                    </v-dialog>
                </div>
                <div class="checklist box">
                    <img src="@/assets/solucoes2.png" alt="Checklist"/>
                    <h>Checklist</h>
                    <span class="button-solucoes" id="detalhes-ck" @click="detalhesCK = true">Ver detalhes</span>
                    <v-dialog v-model="detalhesCK" width="80%">
                            <ChecklistForm></ChecklistForm>
                    </v-dialog>
                </div>
                <div class="laudo-tecnico box">
                    <img src="@/assets/solucoes3.png" alt="Laudo Tecnico"/>
                    <h>Laudo Técnico</h>
                    <span class="button-solucoes" id="detalhes-lt" @click="detalhesLT = true">Ver detalhes</span>
                    <v-dialog v-model="detalhesLT" width="80%">
                            <LaudoTecnicoForm></LaudoTecnicoForm>
                    </v-dialog>
                </div>
            </div>
        </div>
        <div class="footer-box">
            <img src="@/assets/logo-predial-rodape.png" alt="Logo" class="logo"/>
            <div class="footer-text"> 
                <div class="footer-contato">
                    <h>CONTATO</h>
                </div>
                <div class="footer-inf">
                    <p>Predial Consultoria LTDA | CNPJ: xxxxxxxx/xxxx-xx | R. Fatec, 04 | São José dos Campos – SP | CEP 00000-000</p>
                    <p>Contato Suporte: (12)00000-0000 E-mail: suporte@predial.com.br</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    import './style.css'
    import { ref } from 'vue';
    import LaudoTecnicoForm from "./LaudoTecnicoView.vue";
    import ChecklistForm from "./ChecklistView.vue";
    import OrdemServicoForm from "./OrdemServicoView.vue";
        
    let detalhesOS = ref(false);
    let detalhesCK = ref(false);
    let detalhesLT = ref(false);
    console.log(detalhesLT)
</script>
  
```
<p>A página é estruturada em seções, começando com uma introdução sobre o projeto e suas soluções, seguida por cartões que representam as soluções oferecidas pela empresa. Cada cartão possui um botão "Ver detalhes" que abre um modal com informações adicionais sobre a solução.</p>
</details>

<details>
<summary><b>AuthController: Controle de Autenticação</b></summary>
<br>
<p>O código acima implementa o controlador de autenticação (AuthController), responsável por lidar com as solicitações de autenticação dos usuários. Aqui está uma explicação detalhada do que acontece no código:</p>

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.dataTeam.jaia.jaia.model.AuthRequest;
import com.dataTeam.jaia.jaia.service.AuthService;

@RestController
@CrossOrigin
@RequestMapping("/api/auth")
public class AuthController {

    private final AuthService authService;

    @Autowired
    public AuthController(AuthService authService) {
        this.authService = authService;
    }

    @PostMapping("/login")
    public ResponseEntity<String> login(@RequestBody AuthRequest authRequest) {
        String username = authRequest.getUsername();
        String password = authRequest.getPassword();
        String tipoDocumento = authRequest.getTipoDocumento();

        if ("cnpj".equals(tipoDocumento)) {
            String result = authService.authenticateCliente(username, password);
            return ResponseEntity.ok(result);
        } else if ("cpf".equals(tipoDocumento)) {
            String result = authService.authenticateFuncionario(username, password);
            return ResponseEntity.ok(result);
        }

        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body("Tipo de documento inválido");
    }
}
```
<p>O AuthController recebe solicitações POST na rota `/api/auth/login`, onde um objeto `AuthRequest` contendo o nome de usuário, senha e tipo de documento é enviado no corpo da solicitação. Dependendo do tipo de documento (cnpj ou cpf), o método `login()` chama o serviço de autenticação apropriado (`authenticateCliente` ou `authenticateFuncionario`). Se o tipo de documento não for válido, uma resposta de status 400 é retornada.</p>
</details>

## Tecnologias Utilizadas
Spring Boot: Framework utilizado para desenvolver o Back-End do software.

Vue.js: Framework JavaScript utilizado para construir a interface interativa da página.

Oracle SQL: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações sobre usuários e autenticação.

Figma: utilizado para o desenvolvimento e prototipação das wireframes.

## Lições Aprendidas

<p align="justify"></p>

<h3>Hard Skills</h3>
<details>
  <p1>Desenvolvimento Web: Aprofundei meu conhecimento em HTML, CSS e JavaScript, implementando uma landing page responsiva e intuitiva para promover o serviço de inspeção predial.</p1>
  <p1>Vue.js: Aprendi a construir componentes dinâmicos e interativos utilizando o framework Vue.js, proporcionando uma experiência de usuário mais fluida.</p1>
  <p1>Spring Boot: Utilizei o Spring Boot para implementar a lógica de autenticação do sistema, facilitando o desenvolvimento e garantindo a segurança das informações dos usuários.</p1>
  <h3>Soft Skills</h3>
  <p1>Trabalho em Equipe: Colaborei com membros da equipe para definir requisitos, prioridades e prazos, demonstrando habilidades de comunicação e cooperação.</p1>
  <p1>Resolução de Problemas: Enfrentei desafios técnicos durante o desenvolvimento do sistema, buscando soluções eficientes e adaptáveis para garantir a qualidade do produto final.</p1>
  <p1>Gerenciamento de Tempo: Aprendi a gerenciar meu tempo de forma eficaz, equilibrando as demandas do projeto com outras responsabilidades e compromissos pessoais.</p1>
</details>

</details>
<h3>Soft Skills</h3>
<details>
 <p1>Trabalho em Equipe: Colaborei com membros da equipe para definir requisitos, prioridades e prazos, demonstrando habilidades de comunicação e cooperação.</p1>
  <p1>Resolução de Problemas: Enfrentei desafios técnicos durante o desenvolvimento do sistema, buscando soluções eficientes e adaptáveis para garantir a qualidade do produto final.</p1>
  <p1>Gerenciamento de Tempo: Aprendi a gerenciar meu tempo de forma eficaz, equilibrando as demandas do projeto com outras responsabilidades e compromissos pessoais.</p1>
</details>
