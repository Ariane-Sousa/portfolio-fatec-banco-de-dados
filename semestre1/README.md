### Beta
1° Semestre - 01/2022

Parceiro: Professor Fatec - Fabiano Sabha
<p align="center"><img src="beta-logo.png" height=255></img>

## 💻 Nossa proposta

Este projeto foi criado com o objetivo de fornecer uma ferramenta eficaz e acessível para auxiliar alunos em seus estudos diários.
A BETA é uma assistente virtual inteligente, projetada para responder perguntas, fornecer explicações detalhadas, ajudar na organização do tempo de estudo e oferecer recursos educacionais personalizados. Ela utiliza avançados algoritmos de processamento de linguagem natural para entender e responder às necessidades dos alunos de maneira eficiente e intuitiva.

## Lições Aprendidas

<p align="justify"></p>
<h3>Hard Skills</h3>
<details>
  <summary><b>Clique para ver a lista de hard skills</b></summary>
<p1>Desenvolvimento de Software: Fortaleci minhas habilidades em Python criando funcionalidades para a assistente virtual.</p1>

<p1>Uso de Bibliotecas Python: Integrei e utilizei diversas bibliotecas, como SpeechRecognition, Wikipedia, Time, Datetime, Tkinter e Winsound, aprimorando a capacidade da assistente de realizar múltiplas tarefas.</p1>

<p1>Gerenciamento de Projetos: Apliquei a metodologia Scrum para planejamento e execução de sprints, utilizando ferramentas como Trello para gestão de tarefas e GITHUB para controle de versão.</p1>

<p1>Desenvolvimento de Interface: Utilizei Tkinter para criar interfaces gráficas intuitivas e Photoshop para desenvolver e editar elementos visuais.</p1>

<p1>Integração de Sistemas: Desenvolvi habilidades para implementar reconhecimento de voz, e integração com API's.</p1>

</details>
<h3>Soft Skills</h3>
<details>
  <summary><b>Clique para ver a lista de soft skills</b></summary>
<p1>Trabalho em Equipe: A colaboração com a equipe foi fundamental, utilizando Discord para comunicação remota e dividindo responsabilidades de forma eficaz.</p1>

<p1>Gestão do Tempo: Planejei e cumpri prazos conforme cronograma de entregas e sprints, demonstrando habilidades sólidas de gestão do tempo.</p1>

<p1>Comunicação: Desenvolvi habilidades de comunicação ao criar documentação detalhada do projeto e apresentar os resultados na feira de soluções.</p1>

<p1>Resolução de Problemas: Resolvi problemas técnicos e ajustei funcionalidades com base em feedbacks e requisitos do cliente, evidenciando uma abordagem proativa e eficaz.</p1>

</details>

## Contribuições Individuais
<details>
  <summary><b>Reconhecimento de Voz e Execução de Comandos</b></summary>
  <br>
  <p>O código apresentado é parte do desenvolvimento da assistente virtual BETA, que tem como objetivo realizar o reconhecimento de voz e executar comandos baseados nas entradas de áudio do usuário. Aqui está uma explicação detalhada do funcionamento do código:
  </p>
  
```python
import speech_recognition as sr
import wikipedia
import pyttsx3
import time
from tkinter import messagebox
import winsound
from tkinter import *
from tkcalendar import *
import datetime as dt
import pywhatkit
import sounddevice as sd
from scipy.io.wavfile import write
import os
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import A4

audio = sr.Recognizer()
maquina = pyttsx3.init()
maquina.say('Olá, sou a Bêta. Estou aqui para auxiliar.')
maquina.runAndWait()
while True:
    while True:
        with sr.Microphone() as ouvindo:
            print('Ouvindo...')
            voz = audio.listen(ouvindo)
            chamado = audio.recognize_google(voz, language='pt-BR')
            chamado = chamado.lower()
        if chamado == 'beta':
            def executa_comando():
                try:
                    with sr.Microphone() as source:
                        print('Ouvindo...')
                        voz = audio.listen(source)
                        comando = audio.recognize_google(voz, language='pt-BR')
                        comando = comando.lower()
                        if 'beta' in comando:
                            comando = comando.replace('beta', '')
                            maquina.say(comando)
                            maquina.runAndWait()
                except:
                    print('Microfone não está conectado')
                return comando
```
 <p>No código fornecido, o reconhecimento de voz é realizado utilizando a biblioteca `speech_recognition`. A assistente virtual BETA inicia dizendo uma mensagem de boas-vindas através da síntese de voz com `pyttsx3`. Em seguida, entra em um loop infinito para escutar continuamente os comandos do usuário.</p>
  <p>Dentro do loop, o código captura o áudio do microfone e o transforma em texto utilizando o reconhecimento de voz do Google. Se o texto reconhecido for "beta", a função `executa_comando()` é chamada.</p>
  <p>A função `executa_comando()` também captura áudio do microfone e transforma em texto, porém, desta vez, após a detecção do "chamado" inicial. Se o comando contiver a palavra "beta", a assistente repete o comando reconhecido em voz alta.</p>
  <br>
</details>
<details>
  <summary><b>Gravação de Áudio</b></summary>
  <br>
  <p>Neste trecho de código, quando o usuário fala "beta", a assistente inicia a gravação de áudio por 5 segundos. Abaixo está uma explicação detalhada do que acontece:</p>
  
```python
import sounddevice as sd
from scipy.io.wavfile import write
import os

freq = 44100  # Frequência do áudio: 4999 - 64000
seconds = 5  # Duração da gravação

gravacao = sd.rec(int(seconds * freq), samplerate=freq, channels=2)
print("Começando: Fale agora!!")
sd.wait()  # Comando de inicialização da gravação.
print("Fim da gravação!")
write('output.wav', freq, gravacao)  # Salva a gravação como arquivo WAV.
os.startfile("output.wav")           # Abre gravação.
```  
  <p>O código utiliza a biblioteca `sounddevice` para capturar áudio do microfone e `scipy.io.wavfile` para salvar a gravação como arquivo WAV.</p>
  <p>As variáveis `freq` e `seconds` definem a frequência de amostragem do áudio e a duração da gravação, respectivamente. No caso, a gravação dura 5 segundos com uma frequência de 44100 Hz.</p>
  <p>O comando `sd.rec()` inicia a gravação do áudio com base nas configurações especificadas.</p>
  <p>Os comandos `print()` exibem mensagens indicando o início e o fim da gravação.</p>
  <p>O comando `sd.wait()` é responsável por aguardar o término da gravação.</p>
  <p>Após a gravação, o áudio é salvo como um arquivo WAV utilizando o comando `write()`. O arquivo é nomeado como "output.wav".</p>
  <p>Finalmente, o comando `os.startfile()` é usado para abrir o arquivo de áudio recém-gravado, reproduzindo-o no sistema padrão do usuário.</p>
  <br>
</details>

## Tecnologias Utilizadas

Python: Linguagem de programação principal utilizada para desenvolver a lógica da assistente virtual e suas funcionalidades.

Tkinter: Biblioteca gráfica do Python utilizada para criar a interface gráfica da aplicação.

SpeechRecognition: Biblioteca do Python para reconhecimento de voz, utilizada para interpretar comandos de voz do usuário.

Pyttsx3: Biblioteca do Python para síntese de voz, utilizada para que a assistente virtual possa falar com o usuário.
