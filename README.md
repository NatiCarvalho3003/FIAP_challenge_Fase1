# Missão Aurora Siger — Sistema de Verificação de Decolagem

## Descrição do Projeto

Este projeto implementa um sistema de análise de telemetria para validar se uma nave espacial está apta para decolagem.

A partir de um conjunto de dados contendo parâmetros críticos, o algoritmo avalia condições operacionais e determina automaticamente se a missão deve:

* ✅ **DECOLAR**
* ❌ **ABORTAR**

---

## Lógica do Sistema

O sistema segue um protocolo rigoroso baseado em limites operacionais pré-definidos. Caso **qualquer parâmetro esteja fora do intervalo permitido**, a decolagem é automaticamente abortada.

---

## Parâmetros Avaliados

| Variável       | Descrição                    | Condição para DECOLAR |
| -------------- | ---------------------------- | --------------------- |
| `temp_interna` | Temperatura interna          | 18°C a 26°C           |
| `temp_externa` | Temperatura externa          | -100°C a 150°C        |
| `integridade`  | Integridade estrutural       | Igual a 1             |
| `energia`      | Nível de energia             | > 80%                 |
| `pressao_psi`  | Pressão dos tanques          | 450 a 550 PSI         |
| `status`       | Status dos sistemas críticos | Igual a 1             |

---

## Funcionamento do Algoritmo

A função principal:

```python
def analisar_componentes(df: pd.DataFrame):
```

### Etapas:

1. Cria colunas:

   * `Obs`: observações de falhas
   * `decolagem`: status final

2. Percorre cada linha do DataFrame

3. Verifica cada parâmetro:

   * Se estiver fora do padrão → adiciona motivo de falha

4. Resultado final:

   * Se houver falha → `ABORTAR`
   * Caso contrário → `DECOLAR`

---

## Exemplo de Uso

```python
import pandas as pd

df = pd.read_csv('dados_nave.csv')
resultado = analisar_componentes(df)

print(resultado)
```

---

## Estrutura Esperada do Dataset

O arquivo `dados_nave.csv` deve conter as seguintes colunas:

* temp_interna
* temp_externa
* integridade
* energia
* pressao_psi
* status

---

## Análise Energética

O sistema também considera uma análise complementar de energia:

* Capacidade total: **190 kWh**
* Consumo estimado: **20 kWh**
* Perdas: **10%**

### Classificação:

| Energia (kWh) | Status       |
| ------------- | ------------ |
| > 120         | Suficiente   |
| 60 – 120      | Alerta       |
| < 60          | Insuficiente |

---

## Objetivo

Garantir que a decisão de decolagem seja:

* Segura
* Automatizada
* Baseada em dados

---

## Autoria

**Natália Souza Carvalho**
RM: 569068
Turma: 1CCOA
Semestre: 2026/1
