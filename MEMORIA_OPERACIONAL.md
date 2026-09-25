# MEMÓRIA OPERACIONAL — MOTOR DE CADERNOS COMPIERE

**Reescrita do zero em 25/09/2026.** Este arquivo é a ÚNICA fonte. Ignore qualquer memória ou conversa anterior. Só está aqui o que foi testado e aprovado.

---

## 1. ONDE ESTAMOS (resumo)

| Item | Situação |
|---|---|
| Motor no PC | **v13** em `C:\CLAUDE\motor v13` (aprovada e instalada; Pillow + numpy OK). `motor v10` = reserva. |
| Motor na nuvem | **v14** (GitHub `jfsantosdesigner-netizen/motor-cadernos-compiere`, ramo `main` = ramo `v14`). **Aguarda aprovação** para ir ao PC. |
| Versões guardadas | Ramos `v9` … `v14` no GitHub (tags são bloqueadas pela conexão; por isso ramos). |
| Ver cadernos sem baixar | Página privada: https://claude.ai/artifact/XBbud5f2JXjymBFaGjdcYn (4 abas; republicar no mesmo link com `ferramentas/visualizador.py`). |
| Projetos de teste | Caroline Cozinha (8 pr., 38/38) · Felipe Cozinha (8 pr., 30/30) · Rafael Cozinha 2 (10 pr., 41/41) · Rafael Escritório (6 pr., 7/7). Todos em `exemplos/` no repositório. |
| Próximo | **Rafael Claret – SUÍTE CASAL** (`C:\CLAUDE\PROJETO RAFAEL CLARET\SUÍTE CASAL`): gerar com a v14, corrigir o que sair errado. |

---

## 2. PROTOCOLO DE TRABALHO (obrigatório)

1. **PC remoto (Desktop Commander, device JOAO-FELIPE) o MÍNIMO possível** — gasta muitos tokens. Um comando por vez, só para: trazer XML + DXF (zip em base64 num comando só), trazer texturas (só leitura), instalar versão aprovada.
2. **Todo o trabalho é na nuvem**, no repositório do motor. Gerar e conferir lá.
3. **Nada vai para o PC sem o João aprovar.** Instalação = `git clone --depth 1 -b vN` em `C:\CLAUDE\motor vN` (a anterior fica de reserva) + conferir Pillow/numpy.
4. **Toda correção é REGRA do motor**, nunca ajuste só para um projeto.
5. **Cada rodada de correções = nova versão**: atualizar `VERSAO.txt`, caminhos do `padrao.json` (`motor vN`), commit, ramo `vN` no GitHub. Próxima = **v15**.
6. **A cada versão, regerar os 4 projetos de teste** + o novo, e republicar a página de visualização.
7. **Memória fica SÓ na nuvem** (repositório `Compiere`: este arquivo + PDF). Nunca gravar memória no PC.
8. Cadernos para o João ver: sempre pela página (o visualizador de PDF do app falha).

---

## 3. REGRAS DO CADERNO (todas valendo na v14)

### Estrutura
- Sequência: Capa → Contrato → Planta + Especificações → Visão Geral → por bloco: Listagem(ns) → Cotas.
- **Uma letra por parede** (A, B, C, D…; em cada L, a parede maior primeiro).
- **Listagem = uma prancha por parede, 3D BEM FRONTAL** (câmera ~3°), lista SÓ os móveis daquela parede.
- **Parede < 2,5 m**: cotas na mesma prancha da vizinha do L, lado a lado, mesma escala, colunas proporcionais. Parede ≥ 2,5 m = cotas próprias.
- Pranchas = 4 + nº de paredes (listagens) + nº de blocos de cotas.
- Mesma parede com módulos de profundidades diferentes (planos até 600 mm) = uma parede só.

### Imagem 3D da listagem
- Mostra o **ambiente em volta** (móveis vizinhos, pedra, paredes) para orientar; **balões só nos móveis da parede da vista**.
- **Só MDF** (sem dobradiças, suportes, cabideiros, pés). Nada atravessa portas/rodapé (desenho por peça).
- **Paredes reais do DXF** (fundo e laterais, com vão de janela/porta); parede que fica na frente do fundo dos móveis NÃO entra. Móvel ALTO sem parede real atrás → parede de fundo de referência. Ilha/bancada baixa (≤ 1,20 m) não ganha parede inventada.
- Contornos nítidos só com arestas retas reais (nunca diagonais de triangulação).
- **Pedra** com formato real (em L, recorte de cuba), só nas vistas onde ela existe (até 1 m da parede). Sem cota.
- **Eletros/objetos**: só os com forma real (> 12 faces); blocos quadrados NÃO entram; em cima da pedra só o baixo (cuba/cooktop ≤ 300 mm). Sem cota. Rodapé/base solta no chão não é eletro nem parede.
- **Textura real** (veio): a imagem da textura = uma CHAPA de 1830 × 2750 mm (veio nos 2750); cada peça usa o pedaço proporcional ao seu tamanho, veio no sentido do comprimento. Texturas em `texturas/` (1024 px); no PC o motor copia da pasta MATERIAIS a que faltar. Relatório de qualidade avisa textura faltando.
- **Cores reais** pela tabela `materiais_cores.json` (12.971 texturas); não precisa da pasta MATERIAIS de 3 GB.

### Detalhes (quadros embaixo da tabela)
- **NICHO = estrutura ABERTA, SEM PORTA** (sem porta, basculante, gaveta), com ou sem prateleira. **Armário com porta NUNCA é nicho.**
  - Porta detectada pela geometria do DXF: chapa fina na frente cobrindo ≥ 40% do módulo.
  - Vira detalhe: módulo aberto (até 2 m × 1,2 m) + tamponamentos encostados; ou conjunto de painéis/tamponamentos (3+ peças, 2+ horizontais, até 2 m × 1,2 m; peças "Vista" fora). Grupos que se encostam = um detalhe.
  - Nicho maior que 2 m fica na imagem principal.
- **COSTAS**: item listado escondido atrás dos módulos (ex.: painel atrás da ilha) → detalhe visto de trás.
- Balões do detalhe **só no detalhe** (não na imagem grande).
- Quadros ocupam toda a coluna da esquerda, zoom só nas peças do detalhe.
- **Balões nunca sobrepostos** (desloca + traço de chamada), em todas as imagens.

### Cotas (2D frontal, portas abertas)
- Cota **só móveis planejados**. Pedra, eletros, janela, paredes, vizinhos = referência (cinza), NUNCA cotados.
- Cotas externas dos módulos + **cotas internas**: largura livre de cada vão (lateral/divisória) e altura livre entre TODAS as prateleiras, dentro do móvel, texto com fundo branco.
- Alturas a partir do **piso pronto**.
- Escala mínima 1:25 para parede grande; parede/móvel pequeno amplia até **1:20 / 1:15** (ocupando até 75% do espaço).

### Planta (prancha 03)
- Só **móveis e paredes** (sem forro, sanca, pedra, eletros por cima). Paredes em peça única desenhadas pelas faces verticais (vãos abertos). Setas das vistas não se sobrepõem.

### Especificações (prancha 03, modelo fixo do João)
- CORES (caixa, portas/frentes, tamponamentos, painéis/tampos, puxadores, portas de vidro) · FERRAGENS (dobradiças, corrediças, puxadores com NOME EXATO do XML, especiais) · ESPESSURAS (caixa + fundo, prateleiras internas, portas/frentes, tamponamentos, painéis/tampos/perfil). Sem item no projeto = em branco. Texto quebra linha, nunca corta.

---

## 4. FONTE DE DADOS (exportação do Promob)

- **XML MONTADO + DXF** da pasta do ambiente. SketchUp/3DS não são usados; explodido = só Produção Nadecor.
- **DXF com UMA CAMADA POR PEÇA** (o agrupado por cor NÃO serve).
- O DXF pode trazer as paredes da sala numa peça só: o motor lida com isso.
- Para aparecer como referência, **janela, pedra e eletros com forma real precisam vir no DXF**.
- XML não liga portas aos módulos: porta é decidida pela geometria do DXF (o que aparece no 3D vale).

---

## 5. MOTOR — como usar e como está organizado

- **No PC**: arrastar a pasta do ambiente (ex. `PROJETO FULANO\COZINHA`, com XML montado + DXF) no `GERAR_CADERNO.bat` de `C:\CLAUDE\motor vN` → sai `CADERNO - <AMBIENTE>.pdf` + `_QUALIDADE.md` na pasta. Cliente = pasta-mãe sem "PROJETO"; projetista/arquiteta em `padrao.json` ou `dados.json`.
- **Na nuvem**: `python3 gerar_caderno.py exemplos/<PROJETO>/config_nuvem.json` (≈ 5 s por caderno).
- Arquivos principais: `gerar_caderno.py` (tudo), `geo.py` (liga XML↔DXF, paredes), `novo_ambiente.py`, `dxf_pecas.py`, `padrao.json`, `materiais_cores.json`, `texturas/`, `assets/` (LAYOUT_FIXO, CONTRATO, LOGO), `ferramentas/visualizador.py`, `VERSAO.txt`.
- Ferramenta no PC: `C:\CLAUDE\ferramentas\gerar_cores_materiais.py` (gerou a tabela de cores).

---

## 6. NÃO FAZER (testado e reprovado / substituído)

- 3D na diagonal pegando duas paredes na listagem (paredes na frente dos móveis) → **reprovado**.
- "Nicho suspenso" (armário sobre geladeira vira detalhe mesmo com porta) → **errado**, substituído pela definição de nicho aberto.
- Caixa (bbox) de parede em peça única → cobria tudo; usar faces reais.
- Blocos quadrados de eletro na imagem → poluem; fora.
- Memória no PC, mexer no PC sem aprovação, versões sem número novo.

---

## 7. PENDENTE / PRÓXIMO

1. **Suíte Casal (Rafael Claret)**: trazer XML + DXF de `C:\CLAUDE\PROJETO RAFAEL CLARET\SUÍTE CASAL`, gerar com a v14, analisar o que sair errado (João notou erros), corrigir como regra → v15.
2. João aprovar a v14 → instalar em `C:\CLAUDE\motor v14`.
3. Cotas da planta (prancha 03) ainda amontoadas em todos os projetos.
4. Janela só aparece quando o DXF traz o vão.
