# EVS MINIS — Biosite

Página de links premium da **EVS MINIS**, para responder em `https://evsminis.com/bio/`.

HTML estático único, com CSS e JS embutidos. Sem build, sem framework, sem dependência.

## Para o dev do evsminis.com

Leia **[COMO-SUBIR-NO-SITE.md](COMO-SUBIR-NO-SITE.md)**.

Resumo: copie a pasta [`bio/`](bio) para dentro da pasta de arquivos estáticos do
projeto (normalmente `public/`), commite e deixe o Railway republicar. Nada mais.

Os caminhos dentro do HTML são todos relativos — a pasta funciona em qualquer
subpasta, em qualquer servidor.

## Para editar

- Links dos botões: bloco `EVS_LINKS` no fim de `bio/index.html`
- Imagens: substitua os arquivos em `bio/assets/` mantendo os nomes
- Detalhes: [LEIA-ME-DEPLOY.md](LEIA-ME-DEPLOY.md)

## Conteúdo

```
bio/                  a entrega — copiar esta pasta
├── index.html
├── site.webmanifest
└── assets/
logo/                 logo original (não vai ao ar)
referencia/           referência visual (não vai ao ar)
```
