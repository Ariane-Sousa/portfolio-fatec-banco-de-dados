### Sistema de Inspeções Prediais - Jaia
4° Semestre - 02/2023

Parceiro Acadêmico: Jaia

---

## 💻 Nossa proposta

Diante do cenário urbano atual, que combina construções modernas e históricas, a empresa Jaia enfrentava um desafio significativo: o processo de inspeção predial era demorado e sujeito a imprecisões. Buscando otimizar essa tarefa essencial, a Jaia se empenhou em desenvolver uma solução inovadora.

A proposta da empresa foi criar um software de inspeção predial que pudesse transformar o processo atual, tornando-o mais eficiente e preciso. A plataforma foi pensada para oferecer uma experiência intuitiva, permitindo que os inspetores documentem com precisão detalhes importantes e capturem evidências visuais de maneira eficaz. Além disso, a geração imediata de relatórios apoiaria a tomada de decisões mais ágeis e fundamentadas.

Com o objetivo de melhorar a qualidade e a eficiência das inspeções, a Jaia investiu no desenvolvimento dessa tecnologia, que superou as expectativas iniciais. O impacto do software não se limitou à empresa, mas também contribuiu para elevar o padrão das inspeções prediais, promovendo maior segurança e excelência nas estruturas urbanas.

---

## Modelagem do Banco

### <p align="center">DER</p>
<p align="center"><img src="./model-der.png" widht="20%"></img>

### <p align="center">Mer</p>
<p align="center"><img src="./model-mer.png" widht="20%"></img>

---

## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

- **Desenvolvimento Web**: Aprofundei meu conhecimento em HTML, CSS e JavaScript, implementando uma landing page responsiva e intuitiva para promover o serviço de inspeção predial.
  
- **Vue.js**: Aprendi a construir componentes dinâmicos e interativos utilizando o framework Vue.js, proporcionando uma experiência de usuário mais fluida.

- **Spring Boot**: Utilizei o Spring Boot para implementar a lógica de autenticação do sistema, facilitando o desenvolvimento e garantindo a segurança das informações dos usuários.

---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

- **Trabalho em Equipe**: Colaborei com membros da equipe para definir requisitos, prioridades e prazos, demonstrando habilidades de comunicação e cooperação.

- **Resolução de Problemas**: Enfrentei desafios técnicos durante o desenvolvimento do sistema, buscando soluções eficientes e adaptáveis para garantir a qualidade do produto final.

- **Gerenciamento de Tempo**: Aprendi a gerenciar meu tempo de forma eficaz, equilibrando as demandas do projeto com outras responsabilidades e compromissos pessoais.

---

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

---

## Contribuições Coletivas
### Envio de E-mail e PDF
<details> <summary><b>Clique para ver o código e explicação</b></summary>

```java
async function generatePDFAndSendEmail() {
  try {
    const pdfData = await getPdfData();
    const pdfFileName = 'ordem_servico.pdf';
    const email = ordem_servicoSelected.value?.id_req.fk_cliente_id.email;
    if (typeof email === 'string') {
      const assunto = 'Predial - Seja bem-vindo(a) | Ordem de Serviço';
      const corpo = `<p>Olá, ${ordem_servicoSelected.value?.id_req.fk_cliente_id.nome}! Bem-vindo(a) ao Predial!</p>` +
                   `<p>Sua Ordem de Serviço gerada a partir da Requisição: ${ordem_servicoSelected.value?.id_req.nome} Foi Aprovada <br /></p>` +
                   `<p>Segue em anexo o PDF com mais informações: ${pdfFileName}</p>`;
      const formData = new FormData();
      formData.append('recipient', email);
      formData.append('subject', assunto);
      formData.append('body', corpo);
      formData.append('pdfData', new Blob([pdfData], { type: 'application/pdf' }), pdfFileName);
      const response = await axios.post('http://localhost:8080/email/send', formData, {
        headers: {
          'Content-Type': 'multipart/form-data',
        },
      });
      window.alert('E-mail enviado com sucesso!')
    } else {
      window.alert('Endereço de e-mail inválido.');
    }
  } catch (error) {
    console.error(error);
    window.alert('Erro ao enviar o e-mail.');
  }
}
```
Este código implementa a geração de um PDF e o envio de um e-mail para um usuário quando uma Ordem de Serviço é aprovada. Ele utiliza uma função assíncrona para realizar as seguintes etapas:

- Geração do PDF: O código chama a função getPdfData() para obter os dados necessários para a criação do PDF.
- Obtenção do E-mail do Cliente: O e-mail do cliente é extraído a partir de ordem_servicoSelected, que contém os dados da Ordem de Serviço aprovada.
- Preparação do E-mail: O assunto e o corpo do e-mail são configurados, incluindo um texto personalizado com o nome do cliente e informações sobre a ordem de serviço.
- Envio do E-mail: Um FormData é criado contendo o e-mail, assunto, corpo da mensagem e o PDF gerado. Em seguida, a requisição é enviada via axios para um endpoint do backend (/email/send), que provavelmente processa o envio do e-mail com o anexo do PDF.
- Alertas de Sucesso ou Erro: O código exibe alertas para o usuário, informando se o envio do e-mail foi bem-sucedido ou se ocorreu algum erro.
  
Minha contribuição nesse código foi o desenvolvimento da funcionalidade de envio de e-mail e PDF para o usuário. Especificamente, implementei a lógica para garantir que, quando uma Ordem de Serviço fosse aprovada, o cliente recebesse um e-mail com o PDF da ordem gerada, garantindo um processo automatizado e eficiente para comunicação com os clientes.

</details>

---

## **Tecnologias Utilizadas**

- **Spring Boot**: Framework utilizado para desenvolver o Back-End do software, proporcionando uma estrutura robusta e fácil de usar para a construção de APIs e lógica de negócios.
  
- **Vue.js**: Framework JavaScript utilizado para construir a interface interativa da página, proporcionando uma experiência de usuário dinâmica e reativa.

- **Oracle SQL**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações sobre usuários, autenticação e dados do sistema, garantindo alta performance e segurança.

- **Figma**: Ferramenta de design utilizada para o desenvolvimento e prototipação das wireframes, facilitando o processo de criação da interface e alinhamento de ideias com a equipe.

---

## **Conclusão**

Este projeto me permitiu aprimorar minhas habilidades no desenvolvimento de aplicações web, tanto no front-end quanto no back-end. A integração entre o Vue.js para a interface interativa e o Spring Boot no back-end foi fundamental para a criação de uma solução fluida e funcional. 

Além disso, a implementação de processos automatizados como o envio de e-mails com PDFs anexados melhorou a experiência do usuário e garantiu a eficiência no fluxo de trabalho da aplicação. A utilização de Oracle SQL para o gerenciamento de dados proporcionou a segurança e a escalabilidade necessárias para o sucesso do projeto. 

Em resumo, o projeto não só atendeu às necessidades do sistema, mas também me proporcionou um aprendizado significativo em várias tecnologias e metodologias de desenvolvimento
