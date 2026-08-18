# EVS MINIS — Biosite

Página estática única, mobile-first, sem build e sem framework.
Destino: **`https://evsminis.com/bio/`**, dentro do site que seu amigo já hospeda no Railway.

---

## Estrutura

```
dino-carros/
├── bio/                       ← É ESTA PASTA QUE VAI PRO SITE
│   ├── index.html             a página inteira (HTML + CSS + JS)
│   ├── site.webmanifest       ícone ao salvar na tela inicial
│   └── assets/
│       ├── logo.webp          logo principal
│       ├── logo.png           fallback de navegador antigo
│       ├── logo-512.png       ícone do manifest
│       ├── icon-180.png       ícone iOS
│       ├── favicon.png
│       ├── car.webp / car.jpg foto da seção automotiva
│       ├── car-small.jpg      versão leve
│       └── og.jpg             prévia de compartilhamento
│
├── COMO-SUBIR-NO-SITE.md      ← MANDE ISTO PRO SEU AMIGO
├── LEIA-ME-DEPLOY.md          este arquivo
├── logo/                      original que você enviou — não vai ao ar
└── referencia/                referência visual — não vai ao ar
```

Todos os caminhos dentro do HTML são **relativos**. A pasta `bio/` funciona sozinha:
abre com duplo clique, funciona em subpasta, funciona em qualquer servidor.

---

## Como entregar

1. Suba este repositório no GitHub.
2. Mande o link pro seu amigo e peça pra ele ler o **`COMO-SUBIR-NO-SITE.md`**.
3. Na prática o trabalho dele é: copiar a pasta `bio/` para dentro da pasta de
   arquivos estáticos do projeto (`public/` na maioria dos casos), commitar e deixar o
   Railway republicar. Uns 2 minutos.

Ele não precisa instalar nada nem mexer nas dependências do site dele.

---

## Ver antes de mandar

Duplo clique em `bio/index.html`. Como os caminhos são relativos, abre direto do
Windows, sem servidor.

---

## Editar os links dos botões

Estão num bloco único no fim de `bio/index.html` — procure por **`EDITE AQUI OS LINKS`**:

```js
var EVS_LINKS = {
  site:      'https://evsminis.com',
  whatsapp:  'https://chat.whatsapp.com/BfuaPtLejXvJANJqoKYTeU',
  rifas:     'https://chat.whatsapp.com/LgFIkHwLARP4u1LeExrXcy',
  instagram: 'https://www.instagram.com/evs_minis/',
  contato:   'https://chat.whatsapp.com/BfuaPtLejXvJANJqoKYTeU'
};
```

Mude só o texto entre aspas. Todos abrem em nova aba automaticamente.

**`contato`** é o WhatsApp do rodapé — hoje aponta para o grupo da comunidade. Se tiver
um número de atendimento direto, troque por `'https://wa.me/5511999999999'` (país + DDD
+ número, só dígitos).

---

## Trocar imagens

Substitua o arquivo em `bio/assets/` mantendo o mesmo nome — nada no código muda.
Se for uma imagem grande, vale reprocessar antes: logo com fundo transparente até
~760px, fotos em JPEG ou WebP qualidade 82.

---

## Como o visual foi montado

- **Fundo**: nenhuma imagem estática. Composição em CSS — gradientes radiais azul e
  vermelho, malha de pontos, linhas de velocidade animadas, partículas em canvas e uma
  vinheta por cima que garante a leitura do texto.
- **Logo**: badge original recortado com fundo transparente, halo azul pulsando atrás e
  anel de luz cyan/vermelho girando devagar.
- **Botões**: vidro escuro + textura de carbono + borda luminosa na cor de cada um. A
  luz atravessa o botão na entrada, no hover e a cada toque no celular. Ao pressionar,
  encolhe e o glow dispara.
- **Seção automotiva**: foto do carro com parallax sutil, camada escura, luz azul de um
  lado e vermelha embaixo.
- **Acessibilidade**: respeita `prefers-reduced-motion` — com "reduzir movimento" ligado
  no celular, animações e partículas somem e o conteúdo aparece direto.

Larguras contempladas no CSS: 320 · 360 · 390 · 430 · tablet · desktop (conteúdo trava
em 500px e vira um cartão centralizado).
