### Beta
**1° Semestre - 01/2022**

**Parceiro:** Professor Fabiano Sabha - Faculdade de Tecnologia de São José dos Campos (FATEC)

<p align="center"><img src="beta-logo.png" height=255></img></p>

## 💻 Nossa proposta

O projeto **BETA** foi desenvolvido com o propósito de criar uma ferramenta acessível e inteligente que pudesse auxiliar alunos em seus estudos diários. 

A **BETA** é uma assistente virtual, equipada com tecnologia de processamento de linguagem natural, capaz de responder perguntas, oferecer explicações detalhadas, organizar o tempo de estudo e fornecer recursos educacionais personalizados. 

Nossa missão era criar uma solução eficiente, intuitiva e de fácil uso para estudantes, utilizando o poder da tecnologia para facilitar o aprendizado e otimizar o desempenho acadêmico.

## Lições Aprendidas

### Hard Skills
<details>
  <summary><b>Clique para ver a lista de hard skills</b></summary>
  
- **Desenvolvimento de Software:** Fortaleci minhas habilidades em Python ao criar funcionalidades essenciais para a assistente virtual.
  
- **Uso de Bibliotecas Python:** Integrei várias bibliotecas como `SpeechRecognition`, `Wikipedia`, `Tkinter` e `Winsound`, aprimorando a capacidade da assistente em realizar múltiplas tarefas simultâneas.
  
- **Gerenciamento de Projetos:** Utilizei a metodologia Scrum para organizar sprints e entregas, gerenciando tarefas com o Trello e versionando o código com GitHub.
  
- **Desenvolvimento de Interface:** Criei interfaces gráficas usando `Tkinter` e editei elementos visuais com Photoshop, garantindo uma experiência amigável para o usuário.
  
- **Integração de Sistemas:** Desenvolvi habilidades de integração de sistemas, implementando reconhecimento de voz e conectando a assistente com APIs externas.
</details>

### Soft Skills
<details>
  <summary><b>Clique para ver a lista de soft skills</b></summary>

- **Trabalho em Equipe:** Colaborei ativamente com minha equipe, usando o Discord para comunicação remota e dividindo responsabilidades de forma eficiente.

- **Gestão do Tempo:** Segui rigorosamente o cronograma de entregas e sprints, demonstrando habilidades de organização e respeito aos prazos.

- **Comunicação:** Produzi documentação detalhada e apresentei o projeto em uma feira de soluções, aprimorando minhas habilidades de comunicação e apresentação.

- **Resolução de Problemas:** Enfrentei e resolvi desafios técnicos, ajustando funcionalidades com base em feedbacks e requisitos, mostrando uma abordagem prática e proativa.
</details>

## Contribuições Individuais

### Reconhecimento de Voz e Execução de Comandos
<details>
  <summary><b>Clique para ver o código e explicação</b></summary>
  
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
Este trecho implementa a lógica de reconhecimento de voz usando a biblioteca speech_recognition. A assistente BETA ouve comandos e, ao detectar a palavra-chave "beta", inicia a execução do comando reconhecido.
</details>

### Gravação de Áudio
<details> <summary><b>Clique para ver o código e explicação</b></summary>
  
```python
import sounddevice as sd
from scipy.io.wavfile import write
import os

freq = 44100
seconds = 5

gravacao = sd.rec(int(seconds * freq), samplerate=freq, channels=2)
print("Começando: Fale agora!!")
sd.wait()
print("Fim da gravação!")
write('output.wav', freq, gravacao)
os.startfile("output.wav")
```

Neste código, o áudio é gravado por 5 segundos e salvo como um arquivo .wav. A biblioteca sounddevice captura o áudio, e a gravação é então reproduzida automaticamente.
</details>

## Tecnologias Utilizadas
- Python: A principal linguagem de programação usada para a lógica e funcionalidades da assistente.
- Tkinter: Biblioteca utilizada para desenvolver a interface gráfica.
- SpeechRecognition: Usada para o reconhecimento de voz e interpretação de comandos.
- Pyttsx3: Biblioteca de síntese de voz para interagir com o usuário por meio de respostas audíveis.

## Conclusão

Este projeto foi um marco fundamental no meu desenvolvimento como desenvolvedor, pois me proporcionou uma visão mais ampla e profunda das várias etapas de criação de um software completo, desde a concepção até a implementação final. Trabalhar na BETA me ensinou a importância de equilibrar a parte técnica com as necessidades reais dos usuários. 

Aprender a integrar diferentes bibliotecas e sistemas, enquanto gerenciava o tempo e as entregas em equipe, foi uma experiência desafiadora e recompensadora. Além disso, a implementação de algoritmos de reconhecimento de voz e a criação de uma interface gráfica amigável me fizeram perceber como a tecnologia pode ser poderosa quando aplicada para facilitar a vida das pessoas. 

A criação da assistente virtual BETA foi um divisor de águas no meu aprendizado. Ela me ajudou a amadurecer tanto tecnicamente quanto em habilidades interpessoais, mostrando como a colaboração, a comunicação e a capacidade de resolver problemas são essenciais para o sucesso de um projeto. Este projeto me preparou para enfrentar desafios maiores, com confiança de que posso aplicar soluções eficazes e inovadoras em futuros desenvolvimentos.

