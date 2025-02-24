# IA900-mslearn-bike-rental
Aprendizado de máquina automatizado para previsão de aluguel de bicicletas


# Explore o Machine Learning Automatizado no Azure Machine Learning

Este projeto explora o uso do **Aprendizado de Máquina Automatizado** no **Azure Machine Learning** para treinar, avaliar, implantar e testar um modelo de aprendizado de máquina. O objetivo é prever o número de aluguéis de bicicletas esperados em um determinado dia, com base em características sazonais e meteorológicas, utilizando um conjunto de dados de histórico de aluguel de bicicletas.

---

## 📋 Pré-requisitos

Para desenvolver este projeto você precisará de:

- Uma assinatura ativa do **Microsoft Azure**.
- Acesso ao **Azure Machine Learning Studio**: [https://ml.azure.com](https://ml.azure.com).
- Conjunto de dados de aluguel de bicicletas: [Baixar aqui](https://aka.ms/bike-rentals).

---

## ⏱️ Duração Estimada

Este exercício leva aproximadamente **35 minutos** para ser concluído.

---

## 🚀 Configuração do Ambiente

### 1. Criar um Workspace do Azure Machine Learning
1. Entre no portal do Azure: [https://portal.azure.com](https://portal.azure.com).
2. Selecione **+ Criar um recurso** e pesquise por **Machine Learning**.
3. Crie um novo workspace com as seguintes configurações:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie ou selecione um existente.
   - **Nome**: Um nome exclusivo para seu workspace.
   - **Região**: Leste dos EUA.
   - **Conta de armazenamento, Cofre de chaves, Application Insights**: Mantenha as configurações padrão.
   - **Registro de contêiner**: Deixe como *nenhum*.
4. Selecione **Examinar + criar** e depois **Criar**.
5. Após a criação, vá para o recurso e clique em **Iniciar estúdio**.

---

## 🤖 Treinando um Modelo com Machine Learning Automatizado

### 1. Preparação do Conjunto de Dados
- Tipo: **Tabela (mltable)**
- Nome: **bike-rentals**
- Descrição: **Historic bike rental data**
- Fonte: **Arquivos locais** (faça o upload dos arquivos baixados anteriormente)

### 2. Configurações da Tarefa
- **Tipo de tarefa**: Regressão
- **Conjunto de dados**: Aluguel de bicicletas
- **Coluna de destino**: `alugueis`
- **Métrica primária**: `NormalizedRootMeanSquaredError`
- **Modelos permitidos**: `RandomForest` e `LightGBM`
- **Máximo de tentativas**: 3
- **Tempo limite do experimento**: 15 minutos
- **Validação**: Divisão de validação de treinamento (10% para validação)
- **Computação**:
  - Tipo: **Sem servidor**
  - Tamanho da VM: **Standard_DS3_V2**

### 3. Enviar Trabalho de Treinamento
- O trabalho iniciará automaticamente. Aguarde até a conclusão.

---

## 📊 Revisar o Melhor Modelo

1. Após a conclusão do treinamento, acesse a guia **Visão geral** do trabalho de ML automatizado.
2. Observe o **Resumo do Melhor Modelo** e selecione o nome do algoritmo para visualizar os detalhes.
3. Na guia **Métricas**, revise:
   - Gráfico de resíduos (diferenças entre valores previstos e reais)
   - Gráfico `predicted_true` (valores previstos vs valores verdadeiros)

---

## 🌐 Implantar e Testar o Modelo

### 1. Implantação
1. Na guia **Modelo**, selecione **Implantar** como **Ponto de Extremidade em Tempo Real**.
2. Configurações:
   - **Máquina Virtual**: `Standard_DS3_v2`
   - **Contagem de instâncias**: `3`
   - **Ponto de extremidade**: Novo (deixe o nome padrão)
3. Aguarde a conclusão da implantação (5 a 10 minutos).

### 2. Testar o Serviço Implantado
1. Acesse **Pontos de Extremidade** e abra o ponto de extremidade **predict-rentals**.
2. Vá para a guia **Teste** e use os seguintes dados de entrada:
```json
{
  "input_data": {
    "columns": [
      "day", "mnth", "year", "season", "holiday", 
      "weekday", "workingday", "weathersit", 
      "temp", "atemp", "hum", "windspeed"
    ],
    "index": [0],
    "data": [[1, 1, 2022, 2, 0, 1, 1, 2, 0.3, 0.3, 0.3, 0.3]]
  }


---
# 🚀 Limpeza do Projeto: Explore o Machine Learning Automatizado no Azure

Após concluir o exercício de aprendizado de máquina automatizado no Azure Machine Learning, é essencial realizar a limpeza dos recursos utilizados para evitar cobranças desnecessárias e otimizar o uso da sua assinatura do Azure. Esta etapa envolve a exclusão de pontos de extremidade e, opcionalmente, do workspace do Azure Machine Learning.

---

## 🧹 O que será Limpo

1. **Ponto de Extremidade**: O serviço Web criado está hospedado em uma **Instância de Contêiner do Azure**. Se você não pretende continuar experimentando, é recomendável excluí-lo para evitar o acúmulo de custos de uso.
2. **Workspace do Azure Machine Learning**: Caso tenha terminado de explorar o Azure Machine Learning, você pode excluir o workspace e os recursos associados. Isso inclui contas de armazenamento, cofre de chaves e Application Insights.

---

## ⚠️ Aviso Importante

A exclusão da computação garante que sua assinatura **não** seja cobrada por recursos de computação. **No entanto**, uma pequena quantia será cobrada pelo armazenamento de dados enquanto o workspace do Azure Machine Learning existir em sua assinatura. 

Certifique-se de:
- Fazer backup de dados e modelos importantes antes de excluir o workspace.
- Confirmar que não há dependências críticas associadas ao workspace ou aos recursos vinculados.

---

## 🔥 Excluindo o Ponto de Extremidade

1. No **Azure Machine Learning Studio**: [https://ml.azure.com](https://ml.azure.com)
2. Vá para o menu **Pontos de Extremidade**.
3. Localize o ponto de extremidade **predict-rentals**.
4. Selecione o ponto de extremidade e clique em **Excluir**.
5. Confirme a exclusão quando solicitado.

Essa ação interrompe o serviço Web e libera a Instância de Contêiner utilizada.

---

## 🗑️ Excluindo o Workspace do Azure Machine Learning (Opcional)

Se você terminou de explorar o Azure Machine Learning, siga estas etapas para excluir o workspace e todos os recursos associados:

1. Acesse o **Portal do Azure**: [https://portal.azure.com](https://portal.azure.com)
2. Navegue até **Grupos de Recursos**.
3. Localize o grupo de recursos utilizado ao criar o workspace do Azure Machine Learning.
4. Selecione o grupo de recursos e clique em **Excluir grupo de recursos**.
5. Digite o **nome do grupo de recursos** para confirmar e clique em **Excluir**.



