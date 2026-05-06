# 🚗 Automação e Otimização de Dados - Frota de Veículos (SP)

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

## 📌 Sobre o Projeto

Este projeto é um script em **Python** desenvolvido para automatizar a extração, filtragem e otimização do histórico de frotas de veículos registrados. O foco principal do projeto foi resolver um gargalo de **performance** na leitura de planilhas muito extensas, transformando consultas lentas em resultados quase instantâneos através da criação de um sistema de "cache" em JSON.

---

## 📊 Dashboard Interativo

O resultado deste processamento de dados pode ser visualizado em tempo real através do dashboard que desenvolvi no Power BI:

👉 [Acesse o Dashboard Interativo Aqui](https://app.powerbi.com/view?r=eyJrIjoiNWVhOWEwNzMtZTQwZS00MTZkLTgyMDQtYWE1MGQ2NjVjM2Q5IiwidCI6ImNmNzJlMmJkLTdhMmItNDc4My1iZGViLTM5ZDU3YjA3Zjc2ZiIsImMiOjR9)

---
---

## ⚠️ O Desafio vs. 💡 A Solução

**O Desafio:**
A base de dados oficial (baixada via web scraping) contendo os registros de veículos possui mais de **5.300 linhas** por arquivo, englobando todas as cidades do estado. Toda vez que o usuário realizava uma nova busca, o sistema precisava processar essa planilha inteira. Isso consumia muito tempo e processamento.

**A Solução (ETL Otimizado):**
1. O código verifica se os dados do mês/ano solicitados já foram processados.
2. Se não, ele usa `requests` e `BeautifulSoup` para buscar e baixar o arquivo oficial automaticamente.
3. Lê as mais de 5.300 linhas **apenas uma vez** utilizando `pandas`.
4. Filtra exclusivamente os dados do município de **São Paulo**.
5. Agrupa os veículos em categorias específicas (Motos, Automóveis, Ônibus, Caminhões, etc.).
6. Salva esse resultado enxuto em um arquivo `.json` no Google Drive.
7. Nas buscas seguintes, o sistema consome diretamente o JSON, reduzindo o tempo de resposta drasticamente.

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

O script foi desenvolvido para rodar no ambiente do **Google Colab** e utiliza as seguintes bibliotecas:

* **Manipulação e Análise de Dados:** `pandas`, `json`
* **Web Scraping e Requisições:** `requests`, `bs4` (BeautifulSoup), `urllib3`, `urllib.parse`
* **Integração de Ambiente:** `google.colab` (Google Drive)
* **Utilitários do Sistema:** `os`, `io` (BytesIO), `datetime`, `warnings`

---

## ⚙️ Funcionalidades Principais

- [x] **Busca Dinâmica:** O usuário informa o ano e (opcionalmente) o mês desejado.
- [x] **Download Automático:** Faz a raspagem (scraping) do site oficial para baixar a base de dados caso não exista localmente.
- [x] **Tratamento de Dados:** Padroniza o nome dos arquivos baixados e as planilhas lidas em memória.
- [x] **Geração de Cache em JSON:** Cria uma versão estruturada e ultra leve da base filtrada para acelerar consultas futuras.

---

##  Como Executar o Projeto

Como este projeto utiliza a biblioteca `google.colab` para montar o Google Drive e salvar os arquivos `.json` diretamente na nuvem, o ideal é rodá-lo dentro do próprio Colab.

1. Faça o upload do arquivo principal (`.ipynb` ou `.py`) para o seu **Google Colab**.
2. Ao rodar a primeira célula, o Colab pedirá permissão para conectar ao seu Google Drive. **Conceda a permissão**.
3. Certifique-se de que as bibliotecas externas estejam instaladas no ambiente (o Colab já possui a maioria, mas você pode garantir rodando o comando abaixo em uma célula):
   ```python
   !pip install pandas requests beautifulsoup4
