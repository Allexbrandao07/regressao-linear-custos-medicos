# Análises de Regressão Linear – Custos Médicos

## Variável de Interesse
**Custo_Saude**

---

## Ordem Recomendada para Verificação dos Pressupostos
1. Análise Exploratória e Tratamento de Outliers (IQR)  
2. Verificação da Linearidade (Dispersão)  
3. Verificação de Multicolinearidade (VIF)  
4. Teste de Autocorrelação (Durbin-Watson)  
5. Teste de Homocedasticidade (Breusch-Pagan)  
6. Teste de Normalidade dos Resíduos (Shapiro-Wilk, Q-Q plot)  
7. Ajuste do Modelo de Regressão Linear  

---

## Análise da Matriz de Correlação

### Critérios para remover variáveis em caso de multicolinearidade:
- Verificar qual variável tem maior correlação com a dependente.  
- Verificar qual possui maior VIF e removê-la.

### Recomendações de interpretação:
- **Cohen (1992):**  
  - |±0,10| → fraca  
  - |±0,30| → moderada  
  - |±0,50| → forte  

- **Rumsey (2023):**  
  - |±1,00| → perfeita  
  - |±0,70| → forte  
  - |±0,50| → moderada  
  - |±0,30| → fraca  
  - 0 → ausência de relação  

---

## 1. Análise Exploratória e Tratamento de Outliers (IQR)
- Outliers encontrados em **Num_Cirurgias** e **Risco_Saude**.  
- Não podem ser removidos, pois parecem eventos raros, não erros.  
- Aplicada transformação logarítmica em **Risco_Saude**.  
  - Redução de linearidade de 0.11 → 0.06.  

---

## 2. Verificação da Linearidade (Dispersão)
Variáveis excluídas por baixa linearidade com **Custo_Saude**:
- Idade_Paciente  
- Idade_Variavel  
- Num_Checkups  

---

## 3. Verificação de Multicolinearidade (VIF)
- Multicolinearidade entre **Risco_Saude** e **Nivel_Atividade_Fisica**.  
- Ambas fracas, mas **Risco_Saude** tem maior VIF → **removida**.  

---

## 4. Teste de Autocorrelação (Durbin-Watson)
- Forte autocorrelação positiva inicialmente.  
- Exclusão de **Idade_Paciente** → valor DW = 1.80 (aceitável).  
- Obs: já seria excluída pela baixa linearidade.  

---

## 5. Teste de Homocedasticidade (Breusch-Pagan)
- Resultado: 0.004 → não homocedástico.  
- Possíveis variáveis a excluir:  
  - Tempo_Hospitalizacao  
  - Num_Cirurgias  
  - Gastos_Ano_Passado (não pode ser removida).  

---

## 6. Teste de Normalidade dos Resíduos
- Resultado: não normal.  
- Decisão: excluir **Num_Cirurgias**.  
- Consequentemente, **Tempo_Hospitalizacao** também foi retirada.  

---

## 7. Ajuste do Modelo de Regressão Linear
- Variáveis como **Num_Medicacoes** e **Historico_Familiar** tiveram *p > 0.05* → removidas.  

### Modelo final:
- IMC  
- Nivel_Atividade_Fisica  
- Gastos_Ano_Passado  
- Num_Consultas  

### Observação:
- **R² = 1** devido à alta linearidade de **Gastos_Ano_Passado** (~1).  
- Normalização/padronização aplicada às variáveis explicativas → ajuste do modelo e remoção de nota de alerta.  

---

## Conclusão
O modelo robusto, atendendo aos pressupostos da regressão linear, deve incluir as variáveis:  
- **Num_Consultas**  
- **Nivel_Atividade_Fisica**  
- **IMC**  
- **Gastos_Ano_Passado**

