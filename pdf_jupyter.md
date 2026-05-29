# 📊 Exportando Jupyter Notebooks para PDF via LaTeX (Guia Definitivo)

Este guia prático foi criado para resolver de uma vez por todas o famoso erro de compilação `nbconvert failed: PDF creating failed` ao tentar exportar notebooks do Jupyter (`.ipynb`) para o formato PDF utilizando o ecossistema LaTeX no Windows.

Se você já se deparou com logs silenciosos que travam o terminal ou avisos sobre fontes matemáticas ausentes (`rsfs10`, `rsfs5`), este passo a passo vai estruturar seu ambiente do zero para que tudo funcione perfeitamente.

---

## 🛠️ Como a engrenagem funciona?

Para que a conversão ocorra, três ferramentas precisam trabalhar em perfeita harmonia:
1. **Jupyter (nbconvert):** Lê o seu arquivo de notebook.
2. **Pandoc:** Atua como um tradutor, transformando o formato do notebook em um documento TeX (`.tex`).
3. **MiKTeX (XeLaTeX):** O motor LaTeX que compila o arquivo `.tex` gerado, baixa as fontes necessárias e entrega o PDF pronto.

---

## 🚀 Passo a Passo da Configuração

### Passo 1: Instalar e Configurar o MiKTeX (Distribuição LaTeX)

O MiKTeX é o coração da compilação de texto, mas ele precisa ser configurado para não travar o Jupyter em segundo plano.

1. Baixe o instalador oficial no site do [MiKTeX](https://miktex.org/download).
2. Durante a instalação, prefira escolher a opção **"Only for me"** (Apenas para mim) para evitar problemas de permissão com o Windows.
3. **Ajuste Crítico (On-the-fly):** Abra o **MiKTeX Console** no menu iniciar, vá em **Settings** (Configurações) e altere a opção *"You can choose whether missing packages are to be installed on-the-fly"* para **Always** (Sempre). 
   > 💡 *Por que isso é necessário?* Por padrão, o MiKTeX tenta abrir uma janela pop-up pedindo permissão para baixar pacotes de fontes que faltam. Como o Jupyter roda o comando de forma oculta (`-quiet`), essa janela nunca aparece, fazendo a conversão travar infinitamente. Configurar para "Always" resolve isso.
4. Vá na aba **Updates** do painel e clique em **Check for updates** para garantir que o gerenciador está totalmente atualizado.

### Passo 2: Instalar o Pandoc

Sem o Pandoc, o Jupyter não consegue sequer iniciar a conversão do arquivo.

1. Acesse o [GitHub oficial do Pandoc](https://github.com/jgm/pandoc/releases).
2. Baixe a versão mais recente do instalador para Windows (procure pelo arquivo com extensão `.msi`, por exemplo: `pandoc-xxx-windows-x86_64.msi`).
3. Siga o fluxo de instalação padrão avançando até o final. O instalador adicionará o executável automaticamente ao `PATH` do seu sistema.

### Passo 3: Atualizar o Ambiente Python

Certifique-se de que as ferramentas de exportação do seu ambiente Python não estão defasadas. Abra o seu **Prompt de Comando (CMD)** ou Terminal do Anaconda e execute:

#### Atualizar o gerenciador de pacotes do Python
python -m pip install --upgrade pip

#### Instalar/Atualizar o ecossistema Jupyter e ferramentas de PDF
pip install --upgrade jupyter nbconvert qtpdf

### Passo 4: Reiniciar o Terminal (Aplicar Variáveis de Ambiente)
Se você acabou de instalar o MiKTeX e o Pandoc:

Feche completamente todas as janelas abertas do Prompt de Comando, Git Bash ou servidores ativos do Jupyter Notebook.

Abra um novo terminal. Isso força o Windows a carregar os novos caminhos do sistema (PATH) criados pelos instaladores.

E pronto, agora basta você ir em File > Download as > PDF via LaTeX (.pdf) e ser feliz com seu documento em mãos.
