# Site da Mandacaru Aerodesign

Este é o site oficial mais atualizado da equipe Mandacaru Aerodesing, equipe de aerodesing da UFPE. Aqui está a apresentação da nossa equipe, nossos patrocinadores e um pouco sobre a história da equipe.

Link do site: https://mandacaruaero.github.io/

---

## Como atualizar o site?
Esse site utiliza o framework **Hugo**, um gerador de sites estático focado em performance e simplicidade.
Optamos por essa tecnologia para garantir que ele seja leve, seguro e fácil de atualizar, permitindo que o foco principal seja na produção de conteúdo e na divulgação de nossas atividades.

Siga os passos a seguir para atualizar os conteúdos do site.
Uso de IA pode ajudar bastante mas é bom revisar e testar antes de publicar.

### 1. Instalação do Ambiente
Para rodar o site localmente, você precisa do **Hugo (Versão Extended)**. A versão "Extended" é obrigatória para processar os estilos (SCSS) do tema **PaperMod**.

---

### Windows
A maneira mais simples é utilizando o gerenciador de pacotes **Winget**, pois não precisa instalar nenhum programa antes.

Execute o o comando:
```bash
winget install Hugo.Hugo.Extended
```

### Linux
O pacote de instalação está disponível no gerenciador de pacotes padrão do seu sistema.


#### Debian e derivados (Ubuntu / Mint / ZorinOS / Pop!_OS):
```bash
sudo apt install hugo
```
#### Fedora
```bash
sudo dnf install hugo
```

Certifique-se de que o comando `hugo version` exibe `extended` na saída.

### MacOS
Usa o gestor de pacotes open-source padrão do sistema, assim como os outros sistemas operacionais
```bash
brew install hugo
```

---

### 2. Clonar o repositório
Abra o terminal e clone o repositório utilizando:
```bash
git clone https://github.com/MandacaruAero/MandacaruAero.github.io.git
```

Depois entre na pasta do repositório e abra em um editor de código para fazer as atualizações.

### 3. Rodar o servidor de desenvolvimento
O Hugo possui um servidor embutido que atualiza o site em tempo real enquanto você edita.
```bash
hugo server -D
```
* O parâmetro `-D` serve para incluir posts marcados como `draft: true` (rascunhos).
* Após o comando, acesse `http://localhost:1313`

### 4. Validar se está tudo certo
Ao navegar pelo site localmente, verifique se:
1. **Estilos**: O layout e as cores do PaperMod aparecem corretamente (se o fundo estiver branco puro e sem formatação, você não instalou a versão Extended).
2. **Imagens**: As fotos da equipe, dos patrocinadores e dos aviões carregam normalmente.
3. **Fórmulas**: Se houver fórmulas matemáticas como $L = \frac{1}{2} \rho v²SC_L$, verifique se elas estão bem renderizadas.
4. **Texto**: Verificar possíveis erros de digitação.

### Comandos Rápidos de Sobrevivência
* **Parar o servidor**: Pressione `Ctrl + C` no terminal
* **Limpar Cache (se algo bugar)**: `rm -rf resources/` e rode o `hugo server` novamente.

## Quais arquivos alterar?
Agora com o ambiente configurado, você pode notar que tem várias pastas e arquivos. Porém, na maioria das vezes, vai ser necessário alterar poucos arquivos de fato.

Os arquivos das páginas do site são os `.md` (Markdown), que representam o corpo do conteúdo. Eles aceitam tanto formatação Markdown tradicional quanto tags HTML misturadas, permitindo bastante flexibilidade.

Aqui estão os principais diretórios com os quais você vai interagir:

### Pasta `content/`
É aqui que ficam os textos das páginas (História, Equipe, Projetos, etc.).
Para editar o texto de uma página específica, basta encontrar o arquivo `.md` correspondente dentro dessa pasta e alterar o seu conteúdo.
*   O Cabeçalho no início de cada arquivo `.md` (entre os `---`) é chamado de **Front Matter**. É lá que definimos o título da página, se ela é um rascunho (indicado pela flag `draft: true`), a data de alteração e outras configurações daquela página específica.

### Pasta `static/` (Imagens e Arquivos)
**Obs**: As imagens possuem um caminho especial. Elas não devem ser referenciadas por caminhos relativos complexos.
* Qualquer arquivo colocado dentro da pasta `static/` será copiado diretamente para a raiz do site final.
* Portanto, se você salvar uma foto da equipe em `static/images/equipe-2026.jpg`, o link correto para usar dentro do seu arquivo `.md` será apenas `/images/equipe-2026.jpg`.

#### Exemplo de como inserir uma imagem no texto:
```Markdown
![Foto da equipe Mandacaru](/images/equipe2026.jpg)
```

### Pasta `assets/css/extended/` (Estilos Customizados)
Se você precisar alterar cores, ajustar o layout padrão do tema PaperMod, ou adicionar alguma estilização específica para a equipe, o arquivo correto para editar é o `custom.css`, localizado em `assets/css/extended/custom.css`.
* Como estamos usando o Hugo na versão **Extended**, ele lê esse arquivo automaticamente e aplica as suas regras de CSS por cima do estilo padrão do site.
* **Regra de Ouro**: Nunca altere os arquivos diretamente dentro da pasta `themes/`. Se o tema for atualizado no futuro, todas as alterações feitas lá serão perdidas. Toda a customização visual da Mandacaru deve ser feita exclusivamente neste arquivo `custom.css`.

### Arquivo de Configuração (`hugo.toml`)
Este é o arquivo central do site. Você só precisará mexer nele se for alterar:
* O nome do site ou a URL base.
* Os links dos menus superiores.
* Configurações globais do tema PaperMod.

### Pasta `layouts/partials/` (Componentes Customizados)
Se for necessário alterar informações do rodapé do site, como mudar os links de contato, ocê deve editar o arquivo `layouts/partials/footer.html`
* **Como funciona**: O Hugo utiliza um sistema de sobreposição. Ao criar esse arquivo na raiz do nosso projeto, o Hugo entende que deve ignorar o rodapé padrão do tema PaperMod e usar o nosso rodapé personalizado.

## Como salvar e publicar as alterações (Deploy)
O nosso site está configurado com **GitHub Actions**. Isso significa que você não precisa compilar o site localmente (gerar a pasta `public/`) para colocar as atualizações no ar. O próprio GitHub faz todo o trabalho de gerar as páginas do Hugo e publicar o site automaticamente assim que o código novo entra no repositório.

Para publicar suas alterações, basta seguir o fluxo padrão do Git para altualizar um repositório.