---
title: README do Projeto para o repositório do Git-hub
tags:
  - ESP32
  - IoT
  - MicroPython
  - Urban-Heat-Island
  - Environmental-Monitoring
  - Sensoriamento_Remoto
Comentários:
  - Projeto ICU-SJ para monitorar Ilhas de Calor Urbano em São José com uma plataforma [[IoT]] de baixo custo, utilizando [[ESP32]] e [[MicroPython]].
Data: 2025-06-24T15:03:00
Autores: Humberto L. Oliveira
alias: [ICU-SJ, Ilhas de Calor São José]
status: em-desenvolvimento

---
# ICU-SJ: Monitoramento de Ilhas de Calor Urbano em São José

![License](https://img.shields.io/badge/license-MIT-blue.svg) ![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow.svg)

>[!info] Info
>Plataforma IoT de baixo custo e alta densidade para o monitoramento, análise e visualização de dados sobre Ilhas de Calor Urbano (ICUs) na cidade de São José.

## 📄 Sobre o Projeto

A região de São José enfrenta o fenômeno das Ilhas de Calor Urbanas (ICUs), que causa impactos diretos na qualidade de vida e no meio ambiente. Um monitoramento local detalhado, com alta cobertura espacial e temporal, é crucial para um planejamento urbano eficaz e para a implementação de estratégias de mitigação.

O projeto **ICU-SJ** propõe uma solução completa e acessível: uma **plataforma IoT ponta-a-ponta**, de baixo custo e alta densidade, projetada para coletar, analisar e visualizar dados microclimáticos em tempo real.

O objetivo é criar uma ferramenta funcional, documentada e replicável que possa complementar os dados de monitoramento existentes, fornecendo informações granulares para pesquisadores, gestores públicos e a comunidade.

### ✨ Principais Funcionalidades

-   **Rede de Nós Sensores de Baixo Custo**: Utilização de microcontroladores ESP32 com sensores de Temperatura, Umidade e Pressão para coleta de dados em campo.
-   **Comunicação em Tempo Real**: Transmissão de dados via Wi-Fi para um backend centralizado na nuvem.
-   **Backend Robusto**: Plataforma na nuvem responsável por receber, armazenar e processar os dados coletados pelos sensores.
-   **Visualização de Dados**: Interface web interativa com mapas de calor e gráficos temporais para facilitar a análise das ICUs.
-   **Projeto Aberto e Replicável**: Toda a documentação de hardware, firmware e software estará disponível para que outras cidades ou pesquisadores possam implementar a solução.

## 🛠️ Tecnologias Utilizadas

- <mark class="hltr-aqua">O projeto é dividido em três componentes principais</mark>:

| Componente   | Tecnologias                                                            |
| :----------- | :--------------------------------------------------------------------- |
| **Hardware** | `ESP32` `Sensor de Temperatura/Umidade/Pressão (T/H/P)`                |
| **Firmware** | `MicroPython` `Python 3` `Thonny IDE`                                  |
| **Backend**  | `[Ex: Node.js/Python]` `[Ex: InfluxDB/MySQL]` `API REST` `MQTT`        |
| **Frontend** | `HTML5` `CSS3` `JavaScript` `[Ex: Leaflet.js/Mapbox]` `[Ex: Chart.js]` |

## 📂 Estrutura do Repositório