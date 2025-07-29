# Análise Espacial das Exportações de Café Arábica em Minas Gerais

## 📋 Descrição

Este repositório contém um script R Markdown que implementa uma metodologia de imputação espacial para estimar as exportações municipais de café arábica (HS6: 090111) em Minas Gerais para o ano de 2023. A análise utiliza o algoritmo desenvolvido por Leal e Martins (2025) para imputar exportações ao nível municipal, combinando dados de comércio exterior com informações de área colhida.

## 🎯 Objetivo

O objetivo principal é estimar as exportações de café arábica por município em Minas Gerais, considerando que os dados oficiais de exportação municipal estão disponíveis apenas no nível de agregação HS4 (café em geral), enquanto necessitamos de estimativas específicas para café arábica (HS6: 090111).

## 📊 Metodologia

A imputação espacial combina dois componentes principais:

1. **Componente Espacial**: Baseado em spillovers de municípios exportadores através de uma matriz de pesos espaciais (inverso da distância)
2. **Componente por Área**: Utiliza a proporção da área colhida municipal como proxy para distribuir o resídual

### Fórmula de Imputação

```
E₆ᵢ = α × Σⱼ wᵢⱼ × E₄ⱼ + rᵢ × (E₆⁻ᴹᴳ - Σᵢ α × Σⱼ wᵢⱼ × E₄ⱼ)
```

Onde:
- `E₆ᵢ` = Exportação municipal imputada (HS6)
- `α` = Fator de conversão HS4 → HS6
- `wᵢⱼ` = Peso espacial entre municípios i e j
- `E₄ⱼ` = Exportação municipal observada (HS4)
- `rᵢ` = Proporção da área colhida municipal
- `E₆⁻ᴹᴳ` = Total estadual de exportações HS6

## 🛠️ Dependências

### Pacotes R Necessários

```r
# Principais pacotes utilizados
pacotes <- c(
  "comexTL",      # Dados de comércio exterior
  "tidyverse",    # Manipulação de dados
  "sf",           # Dados espaciais
  "spdep",        # Econometria espacial
  "ggplot2",      # Gráficos
  "leaflet",      # Mapas interativos
  "plotly",       # Gráficos interativos
  "DT",           # Tabelas interativas
  "kableExtra",   # Formatação de tabelas
  "viridis",      # Paletas de cores
  "geobr"         # Geometrias do Brasil
)
```


## 🚀 Como Executar

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/alanleal-econ/cafe-mg-imputacao.git
   cd cafe-mg-imputacao
   ```

2. **Instale as dependências**:
   ```r
   # O script automaticamente instala os pacotes necessários
   source("cafe_mg.Rmd")
   ```

3. **Execute o script**:
   - Abra o arquivo `cafe_mg.Rmd` no RStudio
   - Execute "Knit to HTML" ou rode os chunks individualmente

## 📈 Resultados Principais

A análise gera os seguintes outputs:

### Visualizações
- **Mapa interativo** das exportações municipais imputadas
- **Gráfico de barras** dos top 10 exportadores
- **Gráfico de pizza** da composição dos componentes
- **Mapa temático** do componente espacial

### Tabelas
- Ranking dos top 15 exportadores municipais
- Estatísticas descritivas da imputação
- Decomposição por componentes

### Métricas Principais
- Cobertura territorial da imputação
- Concentração das exportações
- Validação com dados oficiais estaduais
- Participação de cada componente

## 📊 Dados Utilizados

### Fontes de Dados
1. **SECEX/MDIC**: Dados de exportação municipal (HS4) e estadual (HS6)
2. **PAM/IBGE**: Área colhida de café por município (2023)
3. **IBGE/Geobr**: Geometrias municipais de Minas Gerais

### Variáveis Principais
- Exportações municipais HS4 (código 901 - café)
- Exportações estaduais HS6 (código 090111 - café arábica não torrado)
- Área colhida municipal de café arábica
- Coordenadas geográficas dos municípios

## 🔧 Configurações Técnicas

### Matriz de Pesos Espaciais
- Baseada no **inverso da distância** entre centroides municipais
- Normalizada por linha (matriz estocástica)
- Dimensão: 853 × 853 (todos os municípios de MG)

### Parâmetros de Visualização
- **Tema personalizado** para gráficos (cores em tons de laranja)
- **Mapas interativos** com popups informativos
- **Formatação monetária** em dólares americanos
- **Paletas de cores** viridis/plasma para mapas

## 📝 Citação

Se você utilizar este código ou metodologia, por favor cite:

```
Leal, A. (2025). Análise Espacial das Exportações de Café Arábica em Minas Gerais: 
Imputação e Visualização de Dados Municipais - 2023. 
GitHub: https://github.com/seu-usuario/cafe-mg-imputacao
```

## 👨‍💻 Autor

**Alan Leal**
- Email: [leal@thetalab.com.br]
- GitHub: [@alanleal-econ]
- LinkedIn: [www.linkedin.com/in/alanmarquesleal]

## 📄 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🤝 Contribuições

Contribuições são bem-vindas! Por favor:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📋 Notas Metodológicas

### Validação
- O total imputado corresponde **exatamente** ao valor oficial estadual
- A metodologia preserva a distribuição espacial das exportações
- Os componentes são economicamente interpretáveis

### Limitações
- Baseado em dados de área colhida como proxy de produção
- Assume padrões espaciais estáveis de exportação
- Não considera variações sazonais intra-anuais

### Possíveis Extensões
- Análise temporal (séries históricas)
- Incorporação de outras variáveis explicativas
- Validação com dados primários quando disponíveis
- Extensão para outros produtos agrícolas

---

**Data da última atualização**: 26 de julho de 2025
