# Ligar o app ao Firebase (números iguais em todos os aparelhos)

Leva uns 10 minutos e dá para fazer pelo celular (use o Chrome e ative "Site para computador").

## 1. Criar o projeto
1. Entre em **console.firebase.google.com** com a sua conta Google.
2. Toque em **Criar um projeto** (ou **Add project**), dê um nome (ex.: `privativos-prototipo`) e avance.
3. Pode **desligar o Google Analytics**. Toque em **Criar projeto**.

## 2. Criar o banco de dados
1. No menu do projeto: **Criação > Firestore Database** (ou **Build > Firestore Database**).
2. Toque em **Criar banco de dados**, escolha a região **southamerica-east1 (São Paulo)** e avance.
3. Escolha **Iniciar no modo de produção** e crie.

## 3. Colocar as regras
1. Na tela do Firestore, abra a aba **Regras** (Rules).
2. Apague tudo e cole isto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /entregas/{id} {
      allow read: if request.auth != null;
      allow create: if request.auth != null
                    && request.resource.data.by == request.auth.token.email;
      allow update, delete: if false;
    }
  }
}
```
3. Toque em **Publicar**.

Essas regras só deixam quem está **logado** ler e adicionar entregas. Ninguém consegue editar nem apagar registros pelo app.

## 3b. Ligar o login (um único login e senha)
O app usa **um só login e uma só senha**, que você passa apenas para quem pode usar.
1. No menu do projeto: **Criação > Authentication** e toque em **Vamos começar**.
2. Em **Método de login**, ative **E-mail/senha** (só o primeiro botão, sem "link por e-mail") e salve.
3. Na aba **Usuários**, toque em **Adicionar usuário**:
   - **E-mail:** o login que você quer, seguido de `@privativos.app`. Exemplo: `rouparia@privativos.app`.
   - **Senha:** uma senha forte (mínimo 6 caracteres; use bem mais).
4. No app, as pessoas digitam só o **login** (`rouparia`) e a **senha**. O `@privativos.app` o app completa sozinho.
5. Em **Configurações > Ações do usuário**, desmarque **Ativar criação (cadastro)**, para ninguém criar outra conta. Se a opção não aparecer, confira com a TI.
6. Para trocar a senha ou o login (por exemplo, se alguém que sabia sair da equipe): apague o usuário e crie de novo, ou use o menu de três pontos do usuário > **Redefinir senha** (Reset password / Alterar senha). Depois avise o grupo.

## 4. Pegar a configuração
1. Na página inicial do projeto, toque no ícone **</>** (**Web**) para adicionar um app. Dê um apelido e registre (não precisa marcar Hosting).
2. Vai aparecer um bloco `const firebaseConfig = { ... }`. Copie os valores `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId` e `appId`.

## 5. Colocar a configuração no app
No GitHub, abra o arquivo `firebase-config.js`, toque no lápis (**Edit**) e preencha os campos entre aspas com os valores copiados. Toque em **Commit changes**.

Se preferir, me mande esses valores que eu preencho o arquivo para você.

## 6. Conferir
Abra o endereço do app em dois aparelhos. Vai aparecer a tela **ENTRAR**: use o login e a senha que você criou. Depois de entrar o aparelho continua logado. Para sair: ⋮ > **Sair**. Na tela inicial deve aparecer em verde: **Sincronizado: todos os aparelhos veem os mesmos números**. Registre uma entrega em um e abra o relatório no outro.

## Cuidados importantes
- Com um único login/senha, **não dá para saber qual pessoa fez cada registro** nem tirar o acesso de uma só pessoa: para bloquear alguém, é preciso trocar a senha para todos.
- Use uma senha forte e não coloque ela em nenhum arquivo do GitHub nem em lugar visível.
- Mesmo com login, antes de usar com dados reais de funcionários o hospital (TI/jurídico/LGPD) precisa aprovar onde os dados ficam e quem acessa. Até lá, use **IDs fictícios**.
- Sem internet, o app salva no aparelho e envia os registros sozinho quando a conexão voltar. Para entrar pela primeira vez no aparelho é preciso internet.
- Ao tocar em **Sair**, os registros guardados no aparelho são apagados (os do servidor continuam). Se houver registros ainda sem enviar, o app avisa e não deixa sair.
- Os **dados de demonstração** ficam só no aparelho e não vão para o servidor.
- Como o app não apaga registros do servidor, para limpar os testes use o console do Firebase (Firestore > coleção `entregas` > **Excluir coleção**).
