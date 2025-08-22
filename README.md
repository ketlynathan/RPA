# Prova Final do Curso Avançado de UiPath: Geração de Relatório Anual

Bem-vindo ao repositório da **Prova Final do Curso Avançado de UiPath**, desenvolvido como parte do programa de certificação avançada em automação de processos robóticos (RPA). Este projeto implementa a automação do processo **"Generate Yearly Report for Vendor"**, utilizando o **Robotic Enterprise Framework (REFramework)** da UiPath, com foco em eficiência, escalabilidade e conformidade com as melhores práticas de automação.

## 📋 Descrição do Projeto

Este projeto automatiza o processo de geração de relatórios anuais para fornecedores na empresa fictícia **ACME Systems Inc.**, dentro do departamento de **Finanças e Contabilidade**. A automação consiste em baixar relatórios mensais de um fornecedor específico, com base em seu **Tax ID**, e consolidá-los em um relatório anual no formato Excel, gerando também um **Upload ID** para rastreamento.

### Objetivos da Automação
- **Redução de Tempo**: Acelerar o processamento de relatórios anuais, reduzindo o tempo médio de manuseio de 15 minutos por fornecedor.
- **Aumento de Eficiência**: Automatizar 100% do processo, eliminando atividades manuais demoradas.
- **Confiabilidade**: Garantir precisão e consistência na geração de relatórios, com tratamento robusto de exceções.

### Funcionalidades Principais
- **Download de Relatórios Mensais**: Recuperação automática de relatórios mensais com base no Tax ID do fornecedor.
- **Consolidação de Dados**: Geração de um relatório anual consolidado no formato Excel.
- **Tratamento de Exceções**: Ignora meses com relatórios ausentes (1 a 3 relatórios por fornecedor, conforme especificado).
- **Integração com Orchestrator**: Gerenciamento de filas e ativos para transações e credenciais.
- **Logging e Monitoramento**: Registro detalhado de eventos e captura de screenshots em caso de erros do sistema.

## 🚀 Tecnologias Utilizadas

- **UiPath Studio**: Versão [2022.10].
- **Framework**: Robotic Enterprise Framework (REFramework).
- **Linguagem**: Workflows em XAML, com scripts em VB.NET.
- **Ferramentas de Configuração**: Arquivo `Config.xlsx` para configurações externas e ativos do UiPath Orchestrator.
- **Aplicações**: Sistema interno da ACME Systems Inc. (System 1).
- **Controle de Versão**: Git, hospedado no GitHub.

## 📂 Estrutura do Repositório

O repositório está organizado para facilitar a navegação, manutenção e reutilização do projeto:

```
📦 ProvaFinal_UiPath_GenerateYearlyReport
├── 📂 Config
│   └── Settings.xaml          # Configurações globais do processo
│   └── Config.xlsx           # Parâmetros, incluindo Tax ID e caminhos de arquivos
├── 📂 Data
│   ├── 📂 Input              # Relatórios mensais de entrada (ex.: CSVs, PDFs)
│   ├── 📂 Output             # Relatórios anuais gerados (Excel)
│   └── 📂 Temp               # Arquivos temporários
├── 📂 Framework              # Estrutura do REFramework
│   ├── InitAllSettings.xaml  # Inicialização de configurações
│   ├── GetAppCredentials.xaml # Obtenção de credenciais
│   ├── InitAllApplications.xaml # Abertura do System 1
│   ├── GetTransactionData.xaml # Recuperação de transações
│   ├── SetTransactionStatus.xaml # Atualização de status
│   ├── CloseAllApplications.xaml # Encerramento do System 1
│   └── Main.xaml             # Workflow principal
├── 📂 Workflows              # Workflows específicos do processo
│   ├── Process.xaml          # Lógica de consolidação do relatório anual
│   └── DownloadMonthlyReports.xaml # Download de relatórios mensais
├── 📂 Documentation          # Documentação do projeto
│   └── ProcessDesignDocument.pdf # Documento de design do processo
├── 📄 README.md              # Documentação principal
├── 📄 LICENSE                # Licença do projeto
└── 📄 .gitignore             # Arquivos e pastas ignorados pelo Git
```

## ⚙️ Como Funciona o REFramework

O processo utiliza o **Robotic Enterprise Framework (REFramework)**, estruturado em máquina de estados para gerenciar transações de forma eficiente. Abaixo está o fluxo do processo:

1. **Inicialização do Processo**  
   - **`Framework/InitAllSettings.xaml`**: Carrega configurações do `Config.xlsx` (ex.: Tax ID, caminhos de arquivos) e ativos do Orchestrator.  
   - **`Framework/GetAppCredentials.xaml`**: Recupera credenciais do System 1 via Orchestrator ou Windows Credential Manager.  
   - **`Framework/InitAllApplications.xaml`**: Abre e autentica o System 1.

2. **Obtenção de Dados de Transação**  
   - **`Framework/GetTransactionData.xaml`**: Recupera o Tax ID do fornecedor de uma fila do Orchestrator, conforme definido em `Config("OrchestratorQueueName")`.

3. **Processamento de Transações**  
   - **`Process.xaml`**: Baixa relatórios mensais, consolida os dados em um relatório anual (Excel) e gera o Upload ID.  
   - **`Framework/SetTransactionStatus.xaml`**: Atualiza o status da transação no Orchestrator:  
     - **Sucesso**: Relatório gerado com sucesso.  
     - **Exceção de Regra de Negócio**: Relatórios mensais ausentes (1 a 3 por fornecedor) são ignorados.  
     - **Exceção de Sistema**: Erros técnicos, com captura de screenshots.

4. **Finalização do Processo**  
   - **`Framework/CloseAllApplications.xaml`**: Realiza logout e fecha o System 1.

### Documentação Adicional
Para detalhes completos do processo, consulte o **Process Design Document** na pasta `Documentation`:  
- [Process Design Document](Documentation/ProcessDesignDocument.pdf)  
- [Documentação Oficial do REFramework](https://github.com/UiPath/ReFrameWork/blob/master/Documentation/REFramework%20documentation.pdf)


### Configuração para Novos Projetos
Para adaptar o projeto a outros cenários:
1. **Config.xlsx**: Ajuste os campos para incluir novos fornecedores ou configurações específicas.  
2. **Workflows de Inicialização e Finalização**: Configure `InitAllApplications.xaml` e `CloseAllApplications.xaml` para interagir com outras aplicações.  
3. **Transações**: Modifique `GetTransactionData.xaml` e `SetTransactionStatus.xaml` para outras fontes de dados, se necessário.  
4. **Processamento**: Personalize `Process.xaml` e workflows adicionais para novos processos.

## 📜 Histórico do Documento

O projeto foi desenvolvido com base no **Process Design Document**, revisado e atualizado conforme o histórico abaixo:

| Data       | Versão | Função       | Nome             | Organização       | Comentários         |
|------------|--------|--------------|------------------|-------------------|---------------------|
| 01/08/2017 | 1.0    | Autor        | Olfa Ben Taarit  | ACME Systems Inc. | Criação v1.0        |
| 06/09/2017 | 1.2    | Revisor      | Vrabie Stefan    | UiPath            | Aprovado v1.0       |
| 20/01/2018 | 1.3    | Revisor      | Vrabie Stefan    | UiPath            | Atualizado v1.2     |
| 13/01/2019 | 1.4    | Revisor      | Silviu Predan    | UiPath            | Atualizado v1.3     |

## 📜 Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE). Consulte o arquivo `LICENSE` para mais detalhes.

## 🙌 Agradecimentos

Agradeço à UiPath pelo curso avançado de RPA, que proporcionou o conhecimento necessário para desenvolver esta automação. Agradeço também à equipe da ACME Systems Inc. e à comunidade RPA por compartilhar práticas que enriqueceram este projeto.

