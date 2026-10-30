# 🐢 Jabuti-AGV | Desafio Bosch

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Raspberry Pi](https://img.shields.io/badge/-RaspberryPi-C51A4A?style=for-the-badge&logo=Raspberry-Pi)
![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-660066?style=for-the-badge&logo=mqtt&logoColor=white)

Toda a programação e documentação do projeto **Jabuti-AGV** desenvolvido para o desafio Bosch.

## 📋 Overview do Projeto
O AGV foi modulado com base numa **Raspberry Pi Zero W** com a função de controlo e gestão de stock, visando a redução de recursos humanos despendidos e uma maior autonomia para os armazéns da Bosch.

## 💡 Insights & Tecnologias
O AGV opera como um robô **segue-linha** (utilizando sensor de refletância QRE1113), auxiliado por vários sistemas:
* 🌧️ **Sensor de chuva (FC-37):** Controla a velocidade do AGV com o intuito de preservar a carga.
* 🛑 **Sensor ultrassónico (HC-SR04):** Faz o amparo da locomoção da carga, detetando obstáculos e evitando acidentes.
* 🏷️ **Leitor RFID (MFRC522):** As tags são escritas e posicionadas em pontos específicos para a locomoção do AGV no armazém. Também serve para fazer o controlo das informações de cada carga, enviando esses dados para uma base de dados SQLite.

## 🏗️ Arquitetura e Esquema Elétrico

### Fluxo de Funcionamento
![Arquitetura Desenhada](Arquitetura%20Desenhada.png)

### Diagrama de Ligações (Hardware)
![Esquema Elétrico](Esquema%20Eletrico.png)

## ⚙️ Modelo de Utilização

1. **Recolha (Entrada):** Com o AGV posicionado sobre uma linha projetada, este procurará a leitura do RFID inicial (entrada), onde irá recolher a carga para começar o transporte. 
2. **Identificação:** Assim que a carga é reconhecida, o leitor RFID associa as informações escritas nas TAGS (ID do produto, Nome, Posição e Data de inserção).
3. **Transporte:** O AGV inicia a locomoção. As tags RFID estão posicionadas nas "esquinas" (travessas) de cada secção de stock e em frente a cada prateleira. 
4. **Entrega:** O AGV faz um desvio na rota principal e posiciona-se dentro do stock para que um operador (ou outro robô) remova a carga.
5. **Registo:** Após a remoção, os dados são inseridos na base de dados (via MQTT). O AGV volta ao percurso seguindo instruções contrárias até regressar à posição inicial.

📱 *As informações do stock podem ser apresentadas via telemóvel/aplicação graças ao protocolo MQTT.*

## ⚠️ Notas de Desenvolvimento (Descontinuado)

> **Aviso sobre a câmara OV7670:** O projeto inicialmente seria construído com base numa placa Arduino, mas optámos pela Raspberry Pi para maior potência e facilidade com o MQTT. No entanto, o barramento GPIO da Pi Zero não suporta a alta velocidade de interface necessária (25mb/s) para o módulo da mini-câmara OV7670. Devido a limitações de tempo e compatibilidade de hardware, esta funcionalidade foi removida do protótipo final, mas o escopo da ideia original manteve-se.

## 🎥 Demonstração em Vídeo

[![Vídeo do AGV](https://img.shields.io/badge/YouTube-Assistir_ao_vídeo-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/watch?v=U6FojX3zOjM&list=LL&index=3)
