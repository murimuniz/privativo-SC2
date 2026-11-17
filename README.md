# Privativos (Protótipo)

Protótipo de uma tela de **entrega de privativos** no estilo de um coletor portátil.
Funciona no navegador de qualquer aparelho, **sem internet** depois da primeira abertura. Os registros ficam só no aparelho. (Existe uma ligação opcional com Firebase, desligada por padrão: veja `SETUP-FIREBASE.md`.)

> Protótipo de demonstração. Não está conectado a nenhum sistema do hospital e não faz parte de nenhum sistema oficial.

## O que o app faz

- **Entrega de privativos:** escolhe o setor (UTI, C.C., CME, SND, ENG. CLÍNICA), digita o ID, escolhe a função, marca a(s) cor(es) do privativo e o tamanho (PP até EXG4).
  - Funções: Enfermeiro, Técnico de enfermagem, Médico, Fisio / Instrumentador e Apoio.
  - Cores: Azul, Cinza, Verde e Bege. Ao escolher a função, a cor de costume já vem marcada (enfermeiro azul, técnico cinza, médico verde, apoio bege). Dá para marcar mais de uma.
- **Relatórios:** por dia, tabela de setor × tamanho, totais e lista de entregas por ID.
- **Relatório de cores:** por dia, quantas pessoas de cada função pegaram cada cor e as combinações de cores.
- **Dados de demonstração:** menu **⋮** na tela inicial > *Carregar dados de demonstração* (registros fictícios dos últimos 7 dias, marcados nos relatórios). *Remover dados de demonstração* apaga só os fictícios.

## Como publicar no GitHub (GitHub Pages)

Pelo próprio site do GitHub, sem instalar nada:

1. Entre em [github.com](https://github.com) e clique em **New repository** (o botão verde, ou o **+** no canto superior direito).
2. Dê um nome ao repositório, por exemplo `privativos`. Deixe **Public** marcado e clique em **Create repository**.
3. Na página do repositório, clique em **uploading an existing file** (ou **Add file > Upload files**).
4. Abra a pasta com os arquivos deste projeto e **arraste tudo o que está dentro dela** (não a pasta em si) para a página: `index.html`, `manifest.json`, `sw.js`, `README.md`, `.nojekyll` e a pasta `icons`.
   - Se o navegador não deixar arrastar a pasta `icons`, envie as três imagens dela depois, em **Add file > Upload files**, escrevendo `icons/` no começo do nome, ou crie a pasta pelo botão **Create new file** digitando `icons/` no nome.
5. Clique em **Commit changes**.
6. Vá em **Settings > Pages**. Em **Build and deployment**, escolha **Deploy from a branch**, depois a branch **main** e a pasta **/ (root)**, e clique em **Save**.
7. Espere cerca de 1 a 2 minutos. O endereço aparece no topo da página de Pages e será parecido com:
   `https://SEU-USUARIO.github.io/privativos/`

## Como usar no celular

1. Abra o endereço no **Chrome**.
2. Menu do Chrome (⋮) > **Adicionar à tela inicial** (ou **Instalar app**). O app ganha um ícone e abre em tela cheia.
3. Depois da primeira abertura ele abre mesmo **sem internet**.

## Atualizar o app

No repositório, clique em `index.html` > ícone de lápis (**Edit**) ou **Add file > Upload files** com o arquivo novo, e depois em **Commit changes**. A página é atualizada sozinha em alguns minutos.

## Sobre os dados (importante)

- **Sem Firebase configurado:** os registros ficam somente no navegador do aparelho e nada é enviado para a internet. Cada aparelho tem os seus próprios registros.
- **Com Firebase configurado** (`firebase-config.js` + `SETUP-FIREBASE.md`): as entregas reais vão para o servidor e todos os aparelhos veem os mesmos números. Os dados de demonstração continuam só no aparelho.
- Se você limpar os dados do navegador, os registros daquele aparelho são apagados.
- O repositório é público, então qualquer pessoa com o endereço pode **abrir o app**, mas **não vê os registros que ficam só no aparelho**. Não coloque nomes, IDs reais nem outros dados do hospital nos arquivos do repositório.

## Arquivos

| Arquivo | Para que serve |
| --- | --- |
| `index.html` | O app inteiro (telas, regras e armazenamento) |
| `manifest.json` | Permite instalar o app na tela inicial |
| `firebase-config.js` | Dados de ligação com o servidor Firebase (preencher) |
| `SETUP-FIREBASE.md` | Passo a passo para criar o servidor |
| `sw.js` | Permite abrir o app sem internet |
| `icons/` | Ícones do app |
| `.nojekyll` | Diz ao GitHub Pages para publicar os arquivos como estão |
