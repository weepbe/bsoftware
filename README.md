# B Software — Da ideia à interface

Landing page experimental em que o **scroll conta a história**: uma ideia vira estrutura, design, interface, código, sistema e, por fim, produto digital.

## Rodar localmente

Requisitos: Node 18+.

```bash
npm install
npm run dev        # http://localhost:5173
```

Build de produção:

```bash
npm run build
npm run preview    # http://localhost:4173
```

## Stack

- React 19 + TypeScript + Vite
- GSAP 3 (ScrollTrigger, SplitText, DrawSVG) — timelines controladas pelo scroll (`scrub`)
- Lenis — scroll suave sincronizado com o ticker do GSAP
- Fontes self-hosted via Fontsource: Space Grotesk, Inter, IBM Plex Mono

## Arquitetura

```
src/
  main.tsx                 aguarda as fontes (SplitText mede linhas) e monta o app
  App.tsx                  ordem das cenas + rebuild em resize
  lib/
    gsap.ts                registro de plugins + breakpoints (MQ)
    scroll.ts              Lenis + scrollTo
    scene.ts               scene(): pin + timeline que começa antes do pin (sem telas vazias)
    chapters.ts            store do capítulo ativo (HUD)
    contact.ts             ← e-mail / WhatsApp da B Software
  components/
    Chrome.tsx             nav, grade de fundo, HUD de capítulo e trilho de progresso
    Logo.tsx               marca "B" construída como layout
    SiteMock.tsx           site fictício realmente responsivo (container queries)
    Icons.tsx              ícones e imagem arquitetônica em SVG
  sections/
    Hero                   01  estrutura de linhas que se desmonta
    Idea                   02  palavras espalhadas que se organizam
    Blueprint              03–04 grade → wireframe → interface → produto visual
    Interface              05  desktop → tablet → mobile (a largura real muda)
    Development            06  a interface se abre em camadas 3D
    Systems                07  o site vira um conjunto de janelas de sistema
    Transformation         08  ideia + estrutura + design + tecnologia = produto digital
    Positioning            09  transições tipográficas
    Services               10  lista editorial com microinterações no hover
    Contact                11  CTA final + rodapé
```

Cada cena é uma `section` fixada (pin) com uma timeline `scrub`. Valores por dispositivo ficam em `gsap.matchMedia()` — no mobile as composições mudam (não é só redução).

## Personalizar

- **Contato**: `src/lib/contact.ts`
- **Cores / tipografia**: variáveis em `src/styles/global.css`
- **Ritmo de cada cena**: o segundo argumento de `scene(el, '+=300%')` define quanto scroll a cena dura.

Acessibilidade: com `prefers-reduced-motion`, o scroll suave e as animações CSS são desligados.
