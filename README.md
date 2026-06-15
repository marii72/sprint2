# ☀️ SolarTrack — Sistema de Monitoramento de Energia Solar Fotovoltaica

> **Sprint 2 — Prova de Conceito Funcional**  
> Disciplina: Soluções em Energias Renováveis e Sustentáveis  
> FIAP — 2026

---

##  Integrantes

| Nome | RM |
|---|---|
| Mariana Carminato | 573258 | 
| Gabriel Jurado Nogueira | 571236 |
| Guilherme Garbelini | 571150 |
| Guilherme Henrique de Almeida | 568708 |
| Vinicius Torralles Ferreira Conduta | 570911 |

---

##  Visão Geral do Projeto

O **SolarTrack** é um sistema de monitoramento e análise de geração de energia solar fotovoltaica residencial. A solução coleta (ou simula) dados de painéis solares e apresenta, em tempo real, indicadores de desempenho energético — como potência gerada, energia acumulada, economia financeira e redução de emissões de CO₂.

O objetivo é democratizar o acesso à informação sobre geração de energia limpa, permitindo que o usuário acompanhe a eficiência de seu sistema fotovoltaico e tome decisões conscientes sobre consumo e sustentabilidade.

---

##  Vídeo de Demonstração

 [vou colocar ainda)

---

##  Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                        CAMADA DE DADOS                      │
│   Sensores / Inversor Fotovoltaico → Leitura via protocolo  │
│   (Simulado via script Python em ambiente de prova)         │
└───────────────────────┬─────────────────────────────────────┘
                        │ dados de potência, tensão, corrente
                        ▼
┌─────────────────────────────────────────────────────────────┐
│                   CAMADA DE PROCESSAMENTO                   │
│   simulation.py — gera dados realistas baseados em          │
│   irradiância solar (modelo físico simplificado)            │
│   Cálculo de: kWh gerado, CO₂ evitado, economia em R$       │
└───────────────────────┬─────────────────────────────────────┘
                        │ JSON com métricas processadas
                        ▼
┌─────────────────────────────────────────────────────────────┐
│                   CAMADA DE VISUALIZAÇÃO                    │
│   dashboard.html — interface web com gráficos interativos   │
│   Exibe: curva de geração, totais diários, indicadores      │
│   de sustentabilidade e comparativo de consumo              │
└─────────────────────────────────────────────────────────────┘
```

### Componentes Técnicos

| Componente | Tecnologia | Justificativa |
|---|---|---|
| Simulação física | Python 3 + NumPy | Modelo de irradiância solar baseado no ângulo horário e declinação solar — permite simular qualquer dia/localidade sem hardware real |
| Armazenamento de dados | JSON local | Leve, portátil, suficiente para prova de conceito sem dependência de banco de dados |
| Interface web | HTML5 + Chart.js | Universalmente acessível, sem necessidade de instalação |
| Cálculo de CO₂ | Fator de emissão IPCC | 0,0816 kg CO₂/kWh evitado (fator médio da rede elétrica brasileira — Fonte: IPCC 2021) |

---

##  Instalação e Execução

### Pré-requisitos

- Python 3.8 ou superior
- Navegador web moderno (Chrome, Firefox, Edge)

### Passos

```bash
# 1. Clone o repositório
git clone https://github.com/vinitfc/Solu-es-em-Energias-Renov-veis-e-Sustent-veis-Apresenta-o-do-Projeto-Sustent-vel.git
cd <pasta-do-projeto>

# 2. Instale as dependências Python
pip install numpy

# 3. Execute a simulação (gera o arquivo data.json)
python simulation.py

# 4. Abra o dashboard no navegador
# Abra o arquivo dashboard.html diretamente no navegador
```

---

##  Simulação — Modelo Físico

O script `simulation.py` implementa um modelo simplificado de geração fotovoltaica baseado nos seguintes princípios físicos:

### Irradiância Solar
A potência gerada por um painel solar depende diretamente da irradiância incidente (W/m²). O modelo usa a equação de posição solar:

```
Irradiância(h) = Irradiância_máx × cos(ângulo_zenital(h))
```

Onde o ângulo zenital varia ao longo do dia entre o nascer e o pôr do sol.

### Potência Gerada
```
P(t) = Irradiância(t) × Área_painéis × Eficiência_painel × Fator_temperatura
```

Parâmetros adotados na simulação:
- Área total dos painéis: **6 m²** (4 painéis de 1,5 m² cada)
- Eficiência do painel: **20%** (monocristalino moderno)
- Fator de temperatura: **0,95** (perda típica por aquecimento)
- Pico de irradiância: **1000 W/m²** (STC — Standard Test Conditions)

### Cálculo de Impacto Ambiental
```
CO₂ evitado (kg) = Energia gerada (kWh) × 0,0816 kg/kWh
Árvores equivalentes = CO₂ evitado / 21,77 kg/árvore/ano
```

---

##  Dados Gerados — Exemplo de Saída

Exemplo de dados simulados para um dia típico (21/06, São Paulo — SP):

| Hora | Potência (W) | Energia Acumulada (Wh) | CO₂ Evitado (g) |
|------|-------------|----------------------|-----------------|
| 06:00 | 87 | 0 | 0 |
| 08:00 | 312 | 399 | 32,6 |
| 10:00 | 798 | 1.710 | 139,5 |
| 12:00 | 1.140 | 3.588 | 292,8 |
| 14:00 | 956 | 5.584 | 455,7 |
| 16:00 | 521 | 7.060 | 576,1 |
| 18:00 | 94 | 7.832 | 639,1 |

**Total diário simulado:**
- ⚡ Energia gerada: **7,83 kWh**
- 🌱 CO₂ evitado: **0,64 kg**
- 💰 Economia estimada: **R$ 7,05** (tarifa média R$ 0,90/kWh)

---

##  Princípios de Sustentabilidade e Energias Renováveis

### ODS Relacionadas (ONU)
- **ODS 7** — Energia acessível e limpa: a solução monitora e otimiza geração de energia solar, fonte 100% renovável
- **ODS 13** — Ação contra a mudança do clima: quantifica redução de emissões de CO₂ em tempo real
- **ODS 11** — Cidades e comunidades sustentáveis: democratiza informação sobre energia limpa residencial

### Por que Energia Solar?
A energia solar fotovoltaica é hoje a **fonte de energia mais barata da história**, segundo a Agência Internacional de Energia (IEA, 2023). No Brasil, o potencial solar é extraordinário — São Paulo recebe em média **5,2 kWh/m²/dia** de irradiação global horizontal, o que torna o sistema fotovoltaico residencial viável e com payback entre 4 e 7 anos.

### Eficiência Energética no Sistema
- A simulação permite **identificar horários de pico** de geração, orientando o usuário a deslocar cargas de alto consumo (máquina de lavar, chuveiro elétrico) para essas janelas
- O monitoramento contínuo detecta **degradação de performance** dos painéis, sinalizando necessidade de limpeza ou manutenção antes que a perda se torne significativa
- O painel de CO₂ evitado cria **consciência ambiental mensurável** — converter kWh em árvores ou km de carro torna o impacto tangível para qualquer usuário

---

##  Estrutura do Repositório

```
/
├── README.md               # Este arquivo
├── simulation.py           # Script de simulação do sistema fotovoltaico
├── dashboard.html          # Interface web de visualização dos dados
├── data.json               # Dados gerados pela simulação (exemplo)
└── docs/
    └── arquitetura.png     # Diagrama de arquitetura do sistema
```

---

##  Próximos Passos (Sprint 3)

- Integração com inversor solar real via protocolo Modbus/RS485
- Comparativo entre geração solar e consumo da residência
- Alertas automáticos por e-mail quando a eficiência cair abaixo do esperado
- Previsão de geração baseada em forecast de irradiância (API meteorológica)

---

##  Referências

- IPCC (2021). Climate Change 2021: The Physical Science Basis. Tabela de fatores de emissão.
- IEA (2023). Renewables 2023. International Energy Agency.
- CRESESB/CEPEL. Atlas Solarimétrico do Brasil. Centro de Referência para Energia Solar e Eólica.
- ANEEL (2024). Tarifas de energia elétrica residencial — Resolução Homologatória.
- Duffie, J. A.; Beckman, W. A. (2013). Solar Engineering of Thermal Processes. 4ª ed. Wiley.
