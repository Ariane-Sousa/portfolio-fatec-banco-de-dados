### Assistente Virtual - Beta
**1° Semestre - 01/2022**

**Parceiro:** Professor Fabiano Sabha - Faculdade de Tecnologia de São José dos Campos (FATEC)

<p align="center"><img src="beta-logo.png" height=255></img></p>

---

## 💻 Nossa proposta

A **BETA** é uma assistente virtual, equipada com tecnologia de processamento de linguagem natural, capaz de responder perguntas, oferecer explicações detalhadas, organizar o tempo de estudo e fornecer recursos educacionais personalizados. 

Nossa missão era criar uma solução eficiente, intuitiva e de fácil uso para estudantes, utilizando o poder da tecnologia para facilitar o aprendizado e otimizar o desempenho acadêmico.

---

## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

- **Desenvolvimento de Software**: Aprofundei meus conhecimentos em Python, criando funcionalidades essenciais para a assistente virtual, como o reconhecimento de voz e a execução de comandos.
  
- **Uso de Bibliotecas Python**: Integrei diversas bibliotecas como `SpeechRecognition`, `Wikipedia`, `Tkinter` e `Winsound` para implementar funcionalidades que permitiram à assistente realizar múltiplas tarefas simultaneamente.
  
- **Gerenciamento de Projetos**: Utilizei a metodologia Scrum para organizar as sprints e as entregas, gerenciando as tarefas no Trello e versionando o código com GitHub, o que garantiu um fluxo de trabalho eficiente.
  
- **Desenvolvimento de Interface Gráfica**: Criei interfaces gráficas amigáveis com a biblioteca `Tkinter`, proporcionando uma experiência de usuário agradável e intuitiva.
  
- **Integração de Sistemas**: Desenvolvi a integração do sistema de reconhecimento de voz com APIs externas, permitindo que a assistente interagisse de forma mais eficiente com o usuário.

---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

- **Trabalho em Equipe**: Trabalhei ativamente com minha equipe, utilizando o Discord para comunicação remota e colaborando na divisão de responsabilidades de forma eficaz.

- **Gestão do Tempo**: Organizei meu tempo de forma eficiente para cumprir os prazos definidos no planejamento das sprints, respeitando rigorosamente os cronogramas de entrega.

- **Comunicação**: Produzi documentação detalhada e apresentei o projeto em uma feira de soluções, melhorando minha capacidade de comunicar ideias de forma clara e objetiva.

- **Resolução de Problemas**: Enfrentei desafios técnicos ao longo do projeto e, com base em feedbacks e requisitos, fiz ajustes nas funcionalidades para melhorar o desempenho da assistente virtual.

---

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

---

## Contribuições Coletivas
### Pomodoro
<details> <summary><b>Clique para ver o código e explicação</b></summary>

```python
 elif 'pomodoro' in comando:

            t_now = dt.datetime.now()  # data e hora atual;

            t_pom = 25 * 60  # tempo de duração do fluxo pomodoro 25m;

            t_delta = dt.timedelta(0, t_pom)  # diferença de tempo;

            t_fut = t_now + t_delta  # hora que o pomodoro termina e começa a pausa;

            delta_sec = 5 * 60  # definição de intervalo;

            t_fin = t_now + dt.timedelta(0, t_pom + delta_sec)  # hora que a pausa termina;

            pomodoro = pyttsx3.init()

            pomodoro.say("Pomodóro iniciado " "\n\nAgora é " + t_now.strftime(

                "%H:%M") + " hrs. \n\nTemporizador definido por 25 minutos")

            pomodoro.runAndWait()

            total_pomodoros = 0

            breaks = 0

            # Looping simples dividido em três seções: Hora pomodoro, intervalo e fim do código;

            while True:

                if dt.datetime.now() < t_fut:

                    print('Pomodóro')

                elif t_fut <= dt.datetime.now():

                    if total_pomodoros in range(3, 100, 5):

                        for i in range(1):
                            winsound.Beep((i + 400), 500)  # Primeiro número é referente ao volume do bip.

                        print('Hora do intervalo! Você tem 25 minutos de descanso.')

                        breaks += 1

                        audio = sr.Recognizer()

                        pomodoro = pyttsx3.init()

                        pomodoro.say('Hora do intervalo!')

                        pomodoro.runAndWait()

                        time.sleep(
                            5)  # Por conta do delay da fala subtrair do tempo de pausa um tempo,então o que era pra ser 25 min ficou 21 min

                        print("Foi")

                    if breaks == 0:

                        for i in range(2):
                            winsound.Beep((i + 400), 700)  # Primeiro número é referente ao volume do bip.

                        print('Hora do intervalo!')

                        breaks += 1

                        audio = sr.Recognizer()

                        pomodoro = pyttsx3.init()

                        pomodoro.say('Hora do intervalo! Você tem 5 minutos de descanso.')

                        pomodoro.runAndWait()

                        time.sleep(
                            5)  # Por conta do delay da fala subtrair do tempo de pausa um tempo,então o que era pra ser 5 min ficou o tempo determinado como 1260 dividido por 5, pra ficar um descanso proporcional.

                    else:

                        print('Fim')

                        breaks = 0

                        for i in range(1):
                            winsound.Beep((i + 400), 700)  # Primeiro número é referente ao volume do bip.

                            audio = sr.Recognizer()

                            pomodoro = pyttsx3.init()

                            pomodoro.say('O intervalo acabou, deseja iniciar um novo pomodóro?')

                            pomodoro.runAndWait()

                        usr_ans = messagebox.askyesno("Fim da primeira sequência do pomodóro",

                                                      "Deseja iniciar outra sequência de pomodóro?")

                        total_pomodoros += 1

                        print(total_pomodoros)

                        if usr_ans == True:

                            t_now = dt.datetime.now()

                            t_fut = t_now + dt.timedelta(0, t_pom)

                            t_fin = t_now + dt.timedelta(0, t_pom + delta_sec)


                        elif usr_ans == False:

                            msg = messagebox.showinfo("Fim do pomodóro",

                                                      "\nVocê completou " + str(total_pomodoros) + " pomodóro(s) hoje!")

                            break

                    print("sleeping")

                    time.sleep(1)

                    t_now = dt.datetime.now()

                    timenow = t_now.strftime("%H:%M")
```

Neste código, implementamos um sistema de Pomodoro, um método de gestão de tempo que alterna entre períodos de foco (25 minutos) e intervalos (5 minutos). O processo se inicia quando o usuário diz "pomodoro" para a assistente virtual. A assistente então inicia um temporizador de 25 minutos, durante o qual a tarefa de "Pomodoro" é executada. Quando o tempo de trabalho termina, a assistente avisa sobre o intervalo.

Minha contribuição neste código foi focada na lógica de tempo para o ciclo Pomodoro, garantindo que os intervalos e os tempos de trabalho fossem corretamente calculados e seguissem a metodologia proposta. Além disso, fui responsável por integrar o reconhecimento da palavra-chave "pomodoro", permitindo que a assistente identificasse e iniciasse o ciclo Pomodoro quando o usuário falasse a palavra.
</details>


---

## Tecnologias Utilizadas

- **Python**: Linguagem de programação principal utilizada para implementar a lógica da assistente virtual, integrando as funcionalidades de reconhecimento de voz, processamento de comandos e interação com o usuário.
  
- **Tkinter**: Biblioteca para criação da interface gráfica, permitindo o desenvolvimento de uma interface simples, mas eficiente, para interação com o usuário.
  
- **SpeechRecognition**: Biblioteca responsável pelo reconhecimento de voz, que possibilita à assistente virtual entender os comandos do usuário e executar ações com base nisso.
  
- **Pyttsx3**: Biblioteca de síntese de voz, utilizada para permitir que a assistente virtual responda ao usuário de forma audível, tornando a experiência mais interativa e acessível.

---

## Conclusão

Este projeto foi um grande desafio, principalmente ao integrar a metodologia Scrum e utilizar o Python para desenvolver um projeto real. Desde a criação do ambiente até a utilização das bibliotecas e a lógica de programação para o sistema, cada etapa exigiu dedicação e aprendizado. Embora desafiador, esse processo foi extremamente enriquecedor e contribuiu significativamente para meu crescimento como desenvolvedora.
