# Como publicar o /bio no evsminis.com

> Este arquivo é pro dev que cuida do `evsminis.com` no Railway.

## O que é

A pasta **`bio/`** deste repositório é uma página estática autocontida — um HTML com
CSS e JS embutidos, mais a pasta `assets/`. **Zero dependência, zero build, zero
framework.** Não instala nada, não roda nada, não muda o `package.json` do site.

O objetivo é que ela responda em **`https://evsminis.com/bio/`**.

## Passo 1 — copiar a pasta

Copie a pasta `bio/` inteira (com o `assets/` dentro) para a pasta de arquivos
estáticos do projeto. Depende do stack:

| Stack | Onde colocar | Resultado |
|---|---|---|
| Next.js | `public/bio/` | `/bio/index.html` |
| Nuxt · Astro · SvelteKit | `public/bio/` | `/bio/` |
| Vite · React · Vue (SPA) | `public/bio/` → sai em `dist/bio/` | `/bio/` |
| Express / Fastify puro | qualquer pasta, ver passo 2 | `/bio/` |
| Laravel / PHP | `public/bio/` | `/bio/` |
| Site estático (Caddy, Nginx, `serve`) | raiz do site | `/bio/` |

Todos os caminhos dentro do HTML são **relativos** (`assets/logo.webp`). Ela funciona
em qualquer subpasta sem precisar editar nada.

## Passo 2 — garantir que `/bio` resolve o `index.html`

A maioria dos servidores estáticos já faz isso. Dois casos que precisam de uma linha:

**Express** — servir a pasta explicitamente:

```js
const path = require('path');
app.use('/bio', express.static(path.join(__dirname, 'bio')));
```

Coloque **antes** de qualquer rota catch-all (`app.get('*', ...)`), senão o app engole
a rota.

**Next.js** — o `public/` não resolve index de subpasta. Em `next.config.js`:

```js
async rewrites() {
  return [{ source: '/bio', destination: '/bio/index.html' }];
}
```

Sem isso, `/bio/` funciona mas `/bio` dá 404.

## Passo 3 — SPA com catch-all (atenção)

Se o site for uma SPA que devolve o `index.html` do app para qualquer rota
desconhecida, `/bio` vai cair no roteador do React/Vue e mostrar a página errada.
Nesse caso, exclua o caminho do fallback:

- **Express**: registre o `express.static('/bio', ...)` antes do catch-all (passo 2).
- **Caddy**: `handle /bio* { root * ./bio ; file_server }` antes do `try_files`.
- **Nginx**: `location ^~ /bio/ { alias /caminho/bio/; index index.html; }`

## Passo 4 — testar

Depois do deploy, abrir:

- `https://evsminis.com/bio/` → a página
- `https://evsminis.com/bio/assets/logo.webp` → deve baixar a imagem
- Mandar `https://evsminis.com/bio/` no WhatsApp → deve aparecer a prévia com a logo

Se a página abrir sem imagem e sem estilo, o servidor está entregando o HTML mas
bloqueando a pasta `assets/` — normalmente é o catch-all do passo 3.

## Observações

- As metatags (`canonical`, `og:url`, `og:image`) já estão fixadas em
  `https://evsminis.com/bio/`. Se o endereço final for outro, é só procurar por
  `evsminis.com` no `bio/index.html` e trocar.
- Nada de cookies, nada de analytics, nada de chamada externa além das fontes do
  Google Fonts.
- Peso total: ~1 MB, quase tudo em imagem com cache longo.
- Para trocar links dos botões depois: bloco `EVS_LINKS` no fim do `bio/index.html`.
