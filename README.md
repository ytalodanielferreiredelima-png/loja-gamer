# LojaGames (LH Games)

Projeto Angular 15 (Angular CLI 15.0.4) com Angular Material e Bootstrap.
Loja de jogos que **consome uma API REST** (json-server) para listar, cadastrar, editar e excluir
produtos, com **login**, **token**, **Guard** e **área restrita**.

## Como executar

Você precisa de três coisas rodando: a API, o front-end e o navegador.

```bash
# 1) instalar as dependências do projeto (uma vez)
npm install

# 2) API fake em http://localhost:3000  (terminal 1)
npm install -g json-server@0.17.4
json-server --watch dbgames.json

# 3) aplicação Angular em http://localhost:4200  (terminal 2)
ng serve
```

Teste a API no navegador/Postman: <http://localhost:3000/produtos>

## Login da área restrita

| Usuário | Senha |
|---------|-------|
| `aluno` | `1234` |

Ao logar é criado um token no `localStorage`. Sem token, qualquer rota `/restrito/...` redireciona para `/login`.
O botão **Sair** (menu da área restrita) apaga o token e volta a mostrar o menu principal.

> Autenticação de demonstração, feita só no front-end para fins didáticos: não use assim em produção.

## Rotas

| Rota | Tela | Protegida |
|------|------|-----------|
| `/inicio` | Vitrine de produtos (dados da API) | não |
| `/login` | Login | não |
| `/restrito/lista` | Lista de produtos (editar / excluir) | **sim** |
| `/restrito/cadastro` | Cadastro de produto | **sim** |
| `/restrito/editar/:id` | Atualização de produto | **sim** |

## Estrutura (src/app)

- `models/` → `Produto.model.ts`, `Usuario.model.ts`
- `produto.service.ts` → GET / POST / PUT / DELETE em `http://localhost:3000/produtos`
- `login.service.ts` → login, logout, token e controle de exibição do menu
- `guard.guard.ts` → `CanActivate` que exige o token
- `inicio/`, `login/`, `menu/`, `rodape/`
- `restrito/` → `lista-produto/`, `cadastro-produto/`, `atualiza-produto/`, `menu-restrito/`, `restrito-routing.module.ts`

## Imagens

As fotos ficam em `src/assets/img`. No campo `foto` do produto vai **apenas o nome do arquivo** (ex.: `jogo1.PNG`).
As imagens que acompanham este projeto são marcadores simples: substitua `banner1-3.PNG`, `jogo1-3.PNG` e `logo.png`
pelas suas, mantendo os mesmos nomes (ou ajuste o `dbgames.json`).

---

*Gerado com [Angular CLI](https://github.com/angular/angular-cli) 15.0.4. Comandos úteis: `ng serve`, `ng build`, `ng generate component nome`.*
