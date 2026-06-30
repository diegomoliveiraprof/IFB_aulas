# Instituto Federal de Educação, Ciência e Tecnologia de Brasília  
**Campus Taguatinga**  
**Autor:** Lucas Tony Magalhães de Araújo  
**Linha de Pesquisa:** Computabilidade e Modelos de Computação  
**Título:** Predição de Risco em Obras Públicas via Fine-Tuning de LLMs  
**Orientador:** Me. Henrique Pereira de Freitas Filho  
**Ano:** 2024  

---

## Sumário
1. Introdução  
   1.1 Contextualização  
   1.2 Análise do Problema  
   1.3 Justificativa  
   1.4 Objetivos  
   1.5 Escopo  
   1.6 Organização do Trabalho  

2. Fundamentação Teórica  
   2.1 Obras Públicas: Conceitos, Características e Importância  
   2.2 Gestão de Obras Públicas e Seus Desafios  
   2.3 Controle e Auditoria Governamental  
   2.4 Contexto do Tribunal de Contas da União (TCU)  
   2.5 Processamento de Linguagem Natural (NLP) e Classificação de Textos  
   2.6 Arquitetura Transformer e Mecanismo de Atenção  
   2.7 Grandes Modelos de Linguagem e Adaptação de Domínio  
   2.8 Transfer Learning e Fine-Tuning  
   2.9 Avaliação de Modelos em Classes Desbalanceadas  
   2.10 Trabalhos Relacionados (Estado da Arte)  

3. Metodologia, Estrutura de Dados, Tecnologias e Cronograma  

---

## 1. Introdução

### 1.1 Contextualização
A infraestrutura e a construção civil pública desempenham papel central no desenvolvimento do Brasil e na qualidade de vida da população. Obras como hospitais, escolas e rodovias são essenciais para garantir serviços básicos à sociedade.  
O Tribunal de Contas da União (TCU) exerce papel vital na auditoria e controle governamental, assegurando a correta aplicação dos recursos públicos.  

No entanto, há um problema crônico: a **paralisação frequente de projetos**. O acompanhamento dessas obras gera um volume massivo de documentos textuais não estruturados (editais, laudos, relatórios), cuja análise depende quase inteiramente da leitura manual dos auditores.  

A Inteligência Artificial (IA), especialmente com o avanço do **Processamento de Linguagem Natural (NLP)** e dos **Grandes Modelos de Linguagem (LLMs)**, pode oferecer uma contribuição decisiva. O presente trabalho propõe aplicar **Fine-Tuning** em modelos de linguagem para classificar riscos de paralisação em obras públicas.

---

### 1.2 Análise do Problema
- Paralisação de obras públicas gera prejuízos socioeconômicos severos.  
- Segundo o **Painel de Obras Paralisadas do TCU (2024)**, milhares de projetos estão parados.  
- Motivos: falhas de planejamento, fraudes licitatórias, irregularidades contratuais.  
- Consequências: desperdício de recursos, degradação precoce das estruturas e privação de serviços básicos.  

A análise manual dos documentos é inviável devido ao volume. O uso de **LLMs comerciais** enfrenta barreiras de custo e infraestrutura.  
A solução proposta: **Fine-Tuning de modelos menores e open-source**, especializados no vocabulário de fiscalização de obras.

---

### 1.3 Justificativa
- Obras paralisadas afetam diretamente a vida dos cidadãos.  
- Detectar fraudes e riscos precocemente pode gerar economia de milhões aos cofres públicos.  
- Contribuição acadêmica: avanço no campo de **NLP aplicado ao português brasileiro** e vocabulários técnicos complexos.  

---

### 1.4 Objetivos

#### Objetivo Geral
Avaliar o desempenho e a viabilidade de LLMs baseados na arquitetura **Transformers**, aplicando **Fine-Tuning** para prever riscos de paralisação e detectar padrões anômalos em documentos de auditoria.

#### Objetivos Específicos
- Extrair e organizar dados do **Painel de Obras Paralisadas do TCU**.  
- Realizar pré-processamento dos textos (limpeza, tokenização, balanceamento).  
- Implementar e treinar modelos adaptados ao português brasileiro (ex.: **BERTimbau**).  
- Validar o modelo com métricas padrão (F1-Score, Precisão, Recall).  

---

### 1.5 Escopo
- Foco: desenvolvimento e avaliação de modelo de NLP para classificação de risco.  
- Dados: exclusivamente do **Painel de Obras Paralisadas do TCU**.  
- Limitação: uso de **Transfer Learning (Fine-Tuning)** em modelos pré-treinados em português.  
- O sistema não substitui o julgamento humano, mas atua como ferramenta de apoio.  

---

### 1.6 Organização do Trabalho
- **Capítulo 1:** Introdução (contexto, problema, justificativa, objetivos, escopo).  
- **Capítulo 2:** Fundamentação teórica (Transformer, BERT, NLP).  
- **Capítulo 3:** Metodologia (coleta de dados, pré-processamento, treinamento, cronograma).  

---


# 2. Fundamentação Teórica

## 2.1 Obras Públicas: Conceitos, Características e Importância
A modelagem de um sistema preditivo baseado em Inteligência Artificial exige uma compreensão do domínio do problema. Antes de submeter os documentos governamentais aos algoritmos de **Processamento de Linguagem Natural (NLP)**, é necessário estabelecer as premissas do objeto de análise.  

Esta seção define formalmente o conceito de obra pública, mapeia o fluxo dos dados textuais gerados durante as contratações e dimensiona os impactos socioeconômicos de sua execução.

---

### 2.1.1 Definição Formal e Papel do Estado
No Brasil, a definição de obra pública está relacionada não só com o dever do governo de atender à população, mas também com aspectos contratuais e de engenharia.  

Segundo a **Lei nº 14.133/2021**, Artigo 6º, inciso XII:

> “obra: toda atividade estabelecida, por força de lei, como privativa das profissões de arquiteto e engenheiro que implica intervenção no meio ambiente por meio de um conjunto harmônico de ações que, agregadas, formam um todo que inova o espaço físico da natureza ou acarreta alteração substancial das características originais de bem imóvel.” (BRASIL, 2021)

Assim, uma obra pública deve ser financiada com recursos do Estado e ter como finalidade atender necessidades da sociedade, trazendo benefícios essenciais como saúde, educação e segurança.

---

### 2.1.2 O Fluxo de Dados no Setor Público
Diferente da construção civil privada, as obras públicas passam por um processo rigoroso de **licitação**, seguindo princípios de publicidade e impessoalidade.  

Cada etapa gera documentos padronizados (editais, contratos, relatórios, planilhas), formando um repositório semiestruturado.  

A **Lei nº 14.133/2021**, Artigo 12, inciso VI, estabelece:

> “os atos serão preferencialmente digitais, de forma a permitir que sejam produzidos, comunicados, armazenados e validados por meio eletrônico.” (BRASIL, 2021)

Esse fluxo digital facilita o uso de IA, mas apresenta desafios: documentos extensos podem ultrapassar a “janela de contexto” dos **LLMs**, dificultando o processamento.

---

### 2.1.3 Impacto Social e Econômico
- **Social:** Obras públicas garantem direitos básicos (saúde, educação, mobilidade, segurança). A paralisação gera prejuízos além do financeiro, afetando principalmente populações mais carentes.  
- **Exemplo:** O abandono da construção de um hospital significa falta de atendimento médico, obrigando cidadãos a buscar serviços em locais distantes.  

- **Econômico:** A interrupção abrupta de contratos causa demissões, retração do consumo e prejuízos ao comércio local.  
  - Recursos já aplicados tornam-se **“custos afundados” (sunk cost)**.  
  - Segundo a **CBIC (2023)**, o maior impacto não é apenas financeiro, mas social: a falha do Estado em entregar o empreendimento à sociedade.

---

## 2.2 Gestão de Obras Públicas e Seus Desafios
A gestão eficiente de infraestruturas governamentais exige coordenação rigorosa entre instâncias administrativas. O ciclo de vida de uma obra pública é composto por etapas burocráticas, técnicas e financeiras.  

---

### 2.2.1 O Ciclo de Vida do Investimento Público
O **TCU** divide o ciclo de vida de uma obra em 10 etapas, conforme a cartilha *Obras Públicas em 10 Passos* (2025):

| Fase | Descrição | Documentos Gerados (alvos para NLP) |
|------|-----------|--------------------------------------|
| 1. Levantamento de Necessidades | Identificação da demanda da população | Planos e diagnósticos sociais |
| 2. Planejamento de Ações | Definição de prioridades frente aos recursos | Estudos de viabilidade, relatórios |
| 3. Estudo Técnico Preliminar | Escolha da melhor solução técnica | Documento ETP, análises de custo |
| 4. Licenciamento Ambiental | Autorizações de órgãos ambientais | Licenças (LP, LI, LO), relatórios |
| 5. Definição do Objeto | Projeto básico e orçamento detalhado | Termos de referência, projetos |
| 6. Captação de Recursos | Convênios e repasses de verba | Planos de trabalho, convênios |
| 7. Licitação | Publicação do edital e escolha da empresa | Editais, atas de julgamento |
| 8. Contratação | Execução da obra | Contratos, diários, relatórios |
| 9. Prestação de Contas | Comprovação do uso correto dos recursos | Relatórios finais, notas fiscais |
| 10. Operação e Manutenção | Conservação após entrega | Manuais, relatórios de inspeção |

**Observação:** As fases preliminares (1 a 7) são cruciais para prevenir desperdícios. A **Definição do Objeto (Etapa 5)** é considerada o maior desafio, pois falhas nessa etapa geram atrasos e paralisações.

---

### 2.2.2 Motivos Principais para as Paralisações
Segundo relatórios do **TCU** e pesquisas recentes:

- **Desequilíbrio econômico-financeiro dos contratos** (≈16% dos casos).  
- **Abandono por parte das empresas contratadas.**  
- **Projetos básicos mal elaborados** pelos municípios, especialmente os de pequeno porte (até 50 mil habitantes), que concentram **77% das obras paralisadas** (GUIDI, 2024).  
- **“Apagão das canetas”**: gestores públicos evitam assinar aditivos por medo de punições, travando o andamento burocrático.  
- **Corrupção:** fraudes licitatórias e superfaturamento levam à aplicação de sanções severas (Lei Anticorrupção), resultando na paralisação imediata das obras (DEVIDES; SILVEIRA, 2020).

---

✅ Agora o capítulo está todo estruturado em **Markdown**, com tabelas e listas bem organizadas. Quer que eu siga formatando também as próximas seções (Controle e Auditoria Governamental, TCU, NLP etc.) no mesmo estilo?

## 2.3 Controle e Auditoria Governamental
Após compreender os desafios estruturais da gestão de obras públicas e os impactos das paralisações, é essencial analisar os mecanismos estatais criados para mitigar esses problemas.  
A auditoria atua como guardiã dos recursos coletivos, evoluindo de processos burocráticos para abordagens tecnológicas avançadas.

---

### 2.3.1 Natureza do Controle e Auditoria
A fiscalização da administração pública garante que o dinheiro seja usado de forma legítima e eficiente.  

Segundo **Maria Sylvia Zanella Di Pietro (2018)**, o controle pode ser dividido em duas frentes:
- **Controle interno:** realizado por órgãos dentro da estrutura de cada Poder (ex.: CGU – Controladoria-Geral da União).  
- **Controle externo:** desempenhado pelo Poder Legislativo com auxílio dos Tribunais de Contas.  

A **Lei nº 14.133/2021** organizou a fiscalização em **linhas de defesa**:
1. **Primeira linha:** servidores, agentes de licitação e autoridades que atuam diretamente na governança.  
2. **Segunda linha:** unidades de assessoramento jurídico e controle interno de cada órgão.  
3. **Terceira linha:** órgãos centrais de controle interno e respectivos Tribunais de Contas.  

Na infraestrutura, a auditoria de obras não é apenas contábil: envolve avaliação técnica multidisciplinar, cruzando dados financeiros, verificação física da obra e análise de editais e contratos.  
O objetivo é garantir que todas as etapas do ciclo de vida do investimento sejam cumpridas, evitando desperdícios e assegurando benefícios sociais.

---

### 2.3.2 A IA como Ferramenta de Fiscalização
Para lidar com o volume massivo de documentos, os órgãos de controle passaram a adotar **Inteligência Artificial (IA)**.  

Exemplos no **TCU**:
- **Alice (Análise de Licitações e Editais)** e **SAO (Sistema de Análise de Orçamentos):** extraem informações de diários oficiais e portais de compras, identificando *tipologias de risco* (padrões textuais e números que indicam sobrepreço ou falhas de planejamento).  
- **Ágata:** utiliza feedback dos auditores para treinar algoritmos de Machine Learning. Os auditores rotulam resultados (falso positivo ou não), permitindo que a rede neural aprenda a classificar textos licitatórios com alta acurácia.  

#### Uso de LLMs
Recentemente, o TCU modernizou sua auditoria com **Grandes Modelos de Linguagem (LLMs)**:
- Criou a plataforma **ChatTCU (2024)**, baseada no **Microsoft Azure OpenAI Service**, garantindo confidencialidade e segurança dos dados.  
- Para reduzir *alucinações* (respostas incorretas), adotou a arquitetura **RAG (Retrieval-Augmented Generation)**:  
  - A pergunta do auditor passa por um motor de busca vetorial.  
  - O sistema recupera documentos internos relevantes.  
  - O modelo gera respostas embasadas nesses textos, evitando invenções.  

Impactos:
- O ChatTCU já atende mais de **1.400 usuários** em análises documentais e pesquisas jurídicas.  
- O TCU criou um **Núcleo de Inteligência Artificial** para evoluir a plataforma.  
- Realizou um chamamento público de **Encomenda Tecnológica (Etec)**, selecionando consórcios como **NeuralMind & Terranova** para agregar novas funcionalidades.

---

## 2.4 O Contexto do Tribunal de Contas da União (TCU)

### 2.4.1 Estatísticas e Impacto Financeiro
Segundo o **Acórdão 2600/2024 do TCU**:
- O Brasil registrou **11.941 obras paralisadas** (52% dos contratos vigentes).  
- Impacto financeiro: **R$ 29,36 bilhões** em investimentos previstos, dos quais **R$ 9 bilhões já foram executados**.  

Problemas adicionais:
- Divergências de nomenclaturas entre sistemas.  
- Exemplo: o **Sismob (Ministério da Saúde)** classificava 1.768 obras como “em cancelamento”, quando deveriam estar como “paralisadas”.  
- Isso mostra que apenas dados tabulares são insuficientes, justificando o uso de **NLP** para interpretar documentos textuais.

---

### 2.4.2 Causas Identificadas pelo Tribunal
O TCU categoriza os motivos das paralisações em três frentes principais (classes alvo para modelagem preditiva):

1. **Deficiência Técnica:** projetos básicos mal elaborados, ausência de estudos de viabilidade, incapacidade técnica dos municípios.  
2. **Deficiências no Fluxo Orçamentário e Financeiro:** atrasos nos repasses federais ou incapacidade financeira dos estados/municípios.  
3. **Abandono pelas Empresas Contratadas:** construtoras vencem licitações com orçamentos insuficientes e desistem após etapas iniciais.  
   - Segundo **Santos & Chianca (2025)**, o desequilíbrio econômico-financeiro responde por **16% dos casos**.

---

## 2.5 Processamento de Linguagem Natural (NLP) e Classificação de Textos
Tradicionalmente, a detecção de fraudes dependia de dados estruturados (planilhas, notas fiscais).  
Hoje, irregularidades aparecem em **textos não estruturados** (editais, termos de referência, memoriais descritivos).  

### Classificação de Textos
- Definição: atribuir automaticamente categorias a documentos textuais (Sebastiani, 2002).  
- Aplicações: análise de sentimento, detecção de spam, identificação de linguagem.  
- Nos LLMs, prever a próxima palavra é uma forma de **classificação de contexto** (Jurafsky & Martin, 2026).  

### Aplicação em Obras Públicas
- **Entrada (x):** laudos e históricos contratuais.  
- **Saída (y):** categorias de paralisação (deficiência técnica, problema financeiro, abandono).  
- Vantagem: transcende buscas por palavras-chave, capturando intenção, semântica e correlações ocultas.  
- Resultado: uma **“auditoria semântica”**, capaz de prever riscos antes do colapso do projeto.

---


## 2.6 A Arquitetura Transformers e o Mecanismo de Atenção
Para processar documentos licitatórios extensos, a rede neural precisa compreender relações semânticas e sintáticas entre palavras distantes no texto.  

Diferente das **Redes Neurais Recorrentes (RNNs)**, que processam dados sequencialmente e sofrem para manter dependências de longo prazo, a arquitetura **Transformer (Vaswani et al., 2017)** processa dados em paralelo.  
Isso permite que codificadores bidirecionais analisem toda a sequência de entrada simultaneamente, conectando qualquer par de posições em tempo constante \(O(1)\).

---

### Self-Attention (Autoatenção)
O motor computacional dos Transformers é o **mecanismo de Self-Attention**, que calcula a importância de cada palavra em relação às demais para construir representações contextualizadas.  

A operação mais utilizada é a **Scaled Dot-Product Attention**, definida como:



\[
Attention(Q, K, V) = softmax\left(\frac{QK^T}{\sqrt{d_k}}\right)V
\]



- **Q (Query):** consulta da palavra atual.  
- **K (Key):** chaves das palavras do contexto.  
- **V (Value):** valores extraídos.  

Na prática, isso permite correlacionar, por exemplo, um **aditivo contratual na página 50** com uma **especificação técnica na página 2**, identificando inconsistências em todo o projeto.

---

### Limitações: Gargalo Quadrático
O cálculo \(QK^T\) exige que cada token se relacione com todos os outros, resultando em complexidade \(O(n^2)\).  
Como contratos e licitações possuem centenas de páginas, esse volume excede o limite típico de **512 tokens** dos modelos baseados em BERT.

---

### Soluções Recentes
Para superar essa barreira, foram desenvolvidas variantes da arquitetura Transformer:

- **Transformer-XL (Dai et al., 2019):**  
  - Introduz recorrência em nível de segmento.  
  - Usa codificação posicional relativa.  
  - Aprende dependências até **80% mais longas** que RNNs tradicionais.  

- **Longformer (Beltagy, Peters & Cohan, 2020):**  
  - Substitui a atenção completa por uma combinação de **atenção esparsa e global**.  
  - Reduz complexidade para \(O(n)\) (escala linear).  
  - Viabiliza o processamento de **milhares de tokens** em uma única passagem.  

Essas modificações tornam possível aplicar Transformers em auditoria governamental, processando laudos e contratos extensos sem fragmentar o contexto.

---

## 2.7 Grandes Modelos de Linguagem e Adaptação de Domínio
A detecção de anomalias em textos governamentais exige modelos robustos e adaptados ao jargão específico da engenharia e do controle externo.  

---

## 2.8 Transfer Learning e Fine-Tuning
Treinar um modelo do zero é inviável devido ao custo computacional.  
A solução é o **Transfer Learning**, que ocorre em duas etapas:

1. **Pré-treinamento (Pretraining):**  
   - O modelo consome bilhões de palavras de textos genéricos.  
   - Exemplo: **BERTimbau**, treinado sobre o corpus **brWaC** (milhões de páginas web brasileiras).  

2. **Fine-Tuning (Ajuste Fino):**  
   - Adiciona uma camada de classificação ao modelo pré-treinado.  
   - Reajusta os pesos da rede com dados reais do **TCU** (editais, laudos, acórdãos).  
   - Permite mapear a linguagem burocrática para classes de risco de paralisação.  

#### Transparência e Explicabilidade
Modelos de auditoria exigem confiança.  
O Fine-Tuning pode ser aliado a **Explainable AI (XAI)**, permitindo visualizar quais palavras ou cláusulas tiveram maior peso na decisão do algoritmo.  
Isso garante rastreabilidade e fundamentação para ações de controle.

---

## 2.9 Avaliação de Modelos em Classes Desbalanceadas
A predição de risco enfrenta o problema do **desbalanceamento de classes**: há muito mais obras regulares do que paralisadas.  

- **Acurácia (Accuracy):** pode ser enganosa.  
  - Exemplo: se 95% das obras são regulares, um classificador que sempre prevê “regular” terá 95% de acurácia, mas falhará em identificar paralisações.  

### Métricas alternativas:
- **Precisão (Precision):** exatidão das predições positivas.  
- **Recall (Revocação):** capacidade de encontrar todos os exemplos positivos.  
- **F1-Score:** média harmônica entre precisão e recall.  

#### Limitações
Segundo Powers (2011), essas métricas são enviesadas, pois ignoram a taxa de acerto da classe negativa.  

### Soluções mais robustas:
- **Curvas ROC e AUC:** úteis, mas menos sensíveis em bases altamente desbalanceadas.  
- **Curvas PR (Precision-Recall):** recomendadas para cenários com forte assimetria.  
- **MCC (Matthews Correlation Coefficient):** penaliza falsos positivos e negativos.  
- **Informedness:** quantifica a probabilidade real de decisão embasada nos dados.  

Essas métricas garantem que o modelo não mascare sua incapacidade de aprendizado sob o viés da classe majoritária.

---

## 2.10 Trabalhos Relacionados (Estado da Arte)
A literatura recente mostra avanços na aplicação de IA em obras públicas:

- **Costa & Bastos (2020):** implantação de sistemas Alice e Ágata no TCU.  
- **Kennedy, Hilal & Momeni (2025):** necessidade de **XAI** para auditoria confiável.  
- **Silva et al. (2024):** desenvolvimento do **ChatTCU** com arquitetura RAG.  
- **Yaseen et al. (2020):** modelos híbridos para prever atrasos em construção civil (dados numéricos).  
- **Erfani & Khanjar (2025):** uso de LLMs em contratos e relatórios financeiros.  
- **Brandão et al. (2024):** aplicação do **BERTimbau** para detectar fraudes em licitações públicas brasileiras.  

### Avanço do presente trabalho
Este projeto propõe o **Fine-Tuning de um modelo nativo open-source** com dados textuais reais do TCU, priorizando métricas robustas contra desbalanceamento.  
Assim, atua como ferramenta preditiva altamente especializada para o controle externo.

---

# 3. Metodologia, Estrutura de Dados, Tecnologias e Cronograma

Neste capítulo, apresenta-se a metodologia adotada para a execução da pesquisa, o modelo de estruturação dos dados que alimentarão o algoritmo, as tecnologias selecionadas para o desenvolvimento do projeto e o cronograma de atividades estipulado para a conclusão do Trabalho de Conclusão de Curso.

---

## 3.1 Metodologia
Diferente do desenvolvimento de sistemas tradicionais, a concepção de um modelo preditivo baseado em **Processamento de Linguagem Natural (NLP)** exige um fluxo de trabalho orientado a dados.  

A metodologia será dividida em **quatro fases principais**, seguindo o pipeline clássico de aprendizado de máquina:

1. **Coleta de Dados e Exploração**  
   - Extração de dados reais do **Painel de Obras Paralisadas do TCU (2024)**.  
   - Mapeamento de variáveis categóricas e raspagem dos documentos textuais associados aos contratos.  

2. **Pré-processamento e Limpeza**  
   - Tratamento dos textos não estruturados.  
   - Remoção de ruídos, stopwords, padronização de caracteres e tokenização.  
   - Aplicação de técnicas de balanceamento de classes (Class Weights, Focal Loss).  

3. **Treinamento e Fine-Tuning**  
   - Importação do modelo pré-treinado **BERTimbau**.  
   - Acoplagem de uma nova camada de classificação (*head*).  
   - Treinamento supervisionado com base nos motivos reais de paralisação extraídos do TCU.  

4. **Avaliação e Validação**  
   - Teste da rede neural em conjunto de dados isolado (*test set*).  
   - Uso de métricas adequadas para classes desbalanceadas:  
     - **Matthews Correlation Coefficient (MCC)**  
     - **Curvas Precision-Recall**  
     - **F1-Score**

---

## 3.2 Estruturação do Dataset e Corpus Textual
As informações serão centralizadas em um **Corpus Textual** e um **Dataset Estruturado**, seguindo o modelo multidimensional clássico (**Star Schema**).  

### Estruturas relacionais:

1. **Tabela Fato (Fato Auditoria)**  
   - `id auditoria` (chave primária)  
   - `id obra`, `id documento` (chaves estrangeiras)  
   - `status obra` (Regular, Atrasada, Paralisada)  
   - `label risco` (variável alvo, conforme Acórdão 2600/2024 do TCU):  
     - 0 = Sem Risco  
     - 1 = Deficiência Técnica  
     - 2 = Deficiências no Fluxo Orçamentário e Financeiro  
     - 3 = Abandono pelas Empresas Contratadas  

2. **Dimensão Obra (Dim Obra)**  
   - `id obra` (chave primária)  
   - `tipo obra` (Edificação, Saneamento, Rodovia etc.)  
   - `município` (localidade da execução)  

3. **Dimensão Documento (Dim Documento)**  
   - `id documento` (chave primária)  
   - `tipo documento` (Edital, Laudo, Acórdão etc.)  
   - `texto documento` (corpus textual completo)  

Durante o pré-processamento, essa estrutura será transformada em **DataFrames** e codificada em **tensores**, que serão injetados na arquitetura Transformers para treinamento.

---

## 3.3 Tecnologias
A stack tecnológica adotada será:

- **Linguagem de Programação:** Python  
- **Bibliotecas de Machine Learning e NLP:**  
  - Hugging Face Transformers (importação do BERT)  
  - PyTorch (cálculo de tensores e otimização da rede)  
- **Processamento e Estruturação de Dados:**  
  - Pandas e NumPy (manipulação de dados tabulares)  
  - Scikit-learn (particionamento do dataset e métricas de avaliação)  
- **Ambiente de Execução:** Google Colab (ou equivalente), com suporte a **GPUs** para o Fine-Tuning de LLMs.

---

## 3.4 Cronograma
O cronograma estipulado para execução e conclusão das etapas do TCC ao longo do semestre letivo está descrito na tabela abaixo:

| Atividades                          | Agosto | Setembro | Outubro | Novembro | Dezembro |
|-------------------------------------|:------:|:--------:|:-------:|:--------:|:--------:|
| Coleta de Dados no Painel do TCU    |   X    |          |         |          |          |
| Estruturação e Pré-processamento    |   X    |    X     |         |          |          |
| Implementação e Fine-Tuning do Modelo |        |    X     |         |          |          |
| Avaliação de Métricas e Validação   |        |          |    X    |    X     |          |
| Redação Final do Artigo/Documento   |        |          |         |    X     |    X     |
| Apresentação e Defesa               |        |          |         |    X     |    X     |

---

