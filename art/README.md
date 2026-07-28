# art/ — arte ORIGINAL do jogo (direção Muramasa)

> Casa da arte AUTORAL do dono. **Separada de propósito** do `spritesheets/` da raiz — aquilo é
> placeholder Duelyst (CC0), o cemitério que estamos substituindo. Aqui só entra o que é NOSSO.

## Onde botar o quê

| Você produziu | Vai em | Por quê |
|---|---|---|
| Fonte editável (`.kra`, `.ase`, `.psd`) | `art/fontes/` | pesado — versionado com cuidado (ver git abaixo) |
| PNG/atlas pronto pro jogo | `art/<categoria>/` (ex.: `art/herois/`, `art/inimigos/`, `art/bosses/`, `art/vfx/`, `art/cenario/`, `art/ui/`) | é o que o jogo carrega |
| Faixa de música/SFX | **`audio/`** (não aqui) | pipeline de áudio próprio |

Os addons `kritaImports` e `aseprite_spritesheet_importer` importam automático de onde o arquivo
estiver — salvou aqui, o Godot já enxerga.

### `art/biomas/` e `art/tiles/` — PLACEHOLDER de IA, feito pra trocar (story 2-43)

O **nome do arquivo é o contrato** (catálogo único em `scenes/bancada/fundo_bioma.gd`):

| Slot | Arquivo | Quem usa |
|---|---|---|
| Fundo do bioma | `art/biomas/sugi_bg_<bioma>.jpg` — `abismo, caverna, costa, desfiladeiro, floresta, luz_corrompida, pico, tempestade` | o fundo com parallax da sala |
| Piso/plataforma | `art/tiles/figma_tile_<elemento>.png` — `agua, corrupta, fogo, luz, mato, raio, sombra, terra, vento` | plataformas + bordas do mundo (o elemento vem do bioma, `data/biomes/`) |

Trocar = **soltar o arquivo novo com o mesmo nome**. O carregador tenta `.png` ANTES de `.jpg`, então
arte final em PNG ganha do placeholder sem tocar em código (os fundos vieram em JPG q92 só por peso:
9,98 MB → 1,5 MB). Escureceu/clareou demais? É uma linha em `data/visual/tuning.json` →
`sala_camadas.background.modulate_hex` (e `sala_camadas.piso.modulate_hex`).

## Git (lição do repo: binário incha rápido — já brigamos 2× com peso)

- PNG/atlas game-ready: **commita normal** (leve, e é o que importa versionar).
- Fonte pesada (`.kra`/`.psd` grande): candidata a **Git LFS** ou `art/fontes/` gitignorado-com-backup —
  o Claude configura quando os fontes começarem a pesar. Por ora, commita e a gente monitora o tamanho.

## Como o dono sabe o que falta: a GALERIA

`data/arte/manifesto.json` (a construir) lista TODO slot de arte com status
`faltando → placeholder → wip → final`, e uma cena-galeria (F5) mostra as miniaturas + contadores.
É o equivalente à galeria do outro projeto — o mapa visual de progresso. Trocou a arte de um slot,
atualiza o status, a galeria reflete.

## Nota de estilo (direção convergindo pra Muramasa)

Traço ukiyo-e / pintura japonesa 2D · silhueta legível · cor chapada-painterly · **movimento fluido**
(onde 2D barato ganha do 3D caro). Cada slot do manifesto carrega a nota de estilo dele — a bíblia
de arte mora junto do inventário.
