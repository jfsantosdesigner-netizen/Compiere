# MEMÓRIA OPERACIONAL — MOTOR DE CADERNOS COMPIERE

**Reescrita do zero em 25/09/2026; atualizada na v15.** Este arquivo é a ÚNICA fonte. Ignore qualquer memória ou conversa anterior. Só está aqui o que foi testado e aprovado.

---

## 1. ONDE ESTAMOS (resumo)

| Item | Situação |
|---|---|
| Motor no PC | **v13** em `C:\CLAUDE\motor v13` (aprovada e instalada; Pillow + numpy OK). `motor v10` = reserva. |
| Motor na nuvem | **v19** (GitHub `jfsantosdesigner-netizen/motor-cadernos-compiere`, ramo `main` = ramo `v19`). **Aguarda aprovação** para ir ao PC (v14–v18 não foram instaladas). |
| Versões guardadas | Ramos `v9` … `v19` no GitHub (tags são bloqueadas pela conexão; por isso ramos). |
| Ver cadernos sem baixar | Página privada: https://claude.ai/artifact/XBbud5f2JXjymBFaGjdcYn (5 abas, Suíte Casal primeiro; republicar no mesmo link com `ferramentas/visualizador.py`). |
| Projetos de teste | Caroline Cozinha (8 pr., 38/38) · Felipe Cozinha (8 pr., 30/30) · Rafael Cozinha 2 (10 pr., 41/41) · Rafael Escritório (6 pr., 7/7, agora com o DXF) · Rafael Suíte Casal (10 pr., 12/12) · Rafael Sala e Varanda (11 pr., 16/18) · Rafael Área de Serviço (6 pr., 10/10) · Priscila Suíte Casal – DESAFIO (15 pr. na v19, 61/63; PDF do João = referência das regras especiais; `C:\CLAUDE\CLIENTES\02_ORIGIN\PRISCILA\SUITE CASAL`). Todos em `exemplos/` no repositório, com o XML+DXF MAIS ATUAL do PC (conferido por hash em 25/09). |
| Próximo | João conferir a v16 na página e aprovar → instalar `C:\CLAUDE\motor v19`. |
| Referência | Cadernos feitos À MÃO pelo João (modelo das imagens): Suíte Casal, Caroline, Felipe, Cozinha 2 (Área de Serviço), Escritório — comparar sempre as imagens do motor com eles. |

---

## 2. PROTOCOLO DE TRABALHO (obrigatório)

1. **PC remoto (Desktop Commander, device JOAO-FELIPE) o MÍNIMO possível** — gasta muitos tokens. Um comando por vez, só para: trazer XML + DXF (zip em base64 num comando só), trazer texturas (só leitura), instalar versão aprovada.
2. **Todo o trabalho é na nuvem**, no repositório do motor. Gerar e conferir lá.
3. **Nada vai para o PC sem o João aprovar.** Instalação = `git clone --depth 1 -b vN` em `C:\CLAUDE\motor vN` (a anterior fica de reserva) + conferir Pillow/numpy.
4. **Toda correção é REGRA do motor**, nunca ajuste só para um projeto.
5. **Cada rodada de correções = nova versão**: atualizar `VERSAO.txt`, caminhos do `padrao.json` (`motor vN`), commit, ramo `vN` no GitHub. Próxima = **v20**.
6. **A cada versão, regerar os 8 projetos de teste (a Priscila testa as regras especiais)** + o novo, e republicar a página de visualização.
7. **Memória fica SÓ na nuvem** (repositório `Compiere`: este arquivo + PDF). Nunca gravar memória no PC.
8. Cadernos para o João ver: sempre pela página (o visualizador de PDF do app falha).

---

## 3. REGRAS DO CADERNO (todas valendo na v15)

**Layout, sequência, capa e listagem estão APROVADOS pelo João — não mudar.** O trabalho agora é nas IMAGENS (3D e cotas) e no tamanho delas dentro do layout.

### Estrutura
- Sequência: Capa → Contrato → Planta + Especificações → Visão Geral → por bloco: Listagem(ns) → Cotas.
- **Uma letra por parede** (A, B, C, D…; em cada L, a parede maior primeiro).
- **Listagem = uma prancha por parede, 3D BEM FRONTAL** (câmera ~3°), lista SÓ os móveis daquela parede.
- **Parede < 2,5 m**: cotas na mesma prancha da vizinha do L, lado a lado, mesma escala, colunas proporcionais. Parede ≥ 2,5 m = cotas próprias.
- Pranchas = 4 + nº de paredes (listagens) + nº de blocos de cotas.
- Peça solta (tamponamento/painel) que não encosta em parede nem módulo, mas encosta (até 60 mm) em outra peça, vai para a parede dessa peça. **Nunca vira vista sozinha.**
- Mesma parede com módulos de profundidades diferentes (planos até 600 mm) = uma parede só.

### Imagem 3D da listagem
- **A imagem PREENCHE o quadro todo** (sem margem branca): móveis com folga de 300 mm, o ambiente (paredes, piso cinza claro) completa e é recortado. Móvel pequeno: enquadramento mínimo 2,2 m × 2,0 m (não vira close).
- Mostra o **ambiente em volta** (móveis vizinhos, pedra, paredes) para orientar; **balões só nos móveis da parede da vista**.
- **Só MDF** (sem dobradiças, suportes, cabideiros, pés). Nada atravessa portas/rodapé (desenho por peça).
- **Paredes reais do DXF** (fundo e laterais, com vão de janela/porta); parede que fica na frente do fundo dos móveis NÃO entra. Móvel ALTO sem parede real atrás → parede de fundo de referência. Ilha/bancada baixa (≤ 1,20 m) não ganha parede inventada.
- Contornos nítidos só com arestas retas reais (nunca diagonais de triangulação).
- **Pedra** com formato real (em L, recorte de cuba), só nas vistas onde ela existe (até 1 m da parede). Sem cota.
- **Eletros/objetos**: só os com forma real (> 12 faces); blocos quadrados NÃO entram; em cima da pedra só o baixo (cuba/cooktop ≤ 300 mm). Sem cota. Rodapé/base solta no chão não é eletro nem parede.
- **Textura real** (veio): a imagem da textura = uma CHAPA de 1830 × 2750 mm (veio nos 2750); cada peça usa o pedaço proporcional ao seu tamanho, veio no sentido do comprimento. Texturas em `texturas/` (1024 px); no PC o motor copia da pasta MATERIAIS a que faltar. Relatório de qualidade avisa textura faltando.
- **Cores reais** pela tabela `materiais_cores.json` (12.971 texturas); não precisa da pasta MATERIAIS de 3 GB. Nome do XML com letra a mais/a menos ou cortado casa igual ("Metallic Sued" = "Metalic Suede"). Material sem cor/textura = INCERTO no relatório.

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
- **A cota NÃO elimina as paredes**: a elevação abre parede a parede (face interna da parede lateral + espessura, até 4 m do móvel; sem parede = 300 mm) e do piso ao TETO (pé-direito do DXF). Parede toda na frente do fundo dos móveis não entra.
- **O desenho preenche a prancha**: maior escala que cabe (1:10, 1:12,5, 1:15, 1:20, 1:25…), mesma escala nas colunas. Móvel pequeno NÃO fica pequeno.
- **Parede sozinha na prancha de cotas → prancha DIVIDIDA: cota FRONTAL à esquerda + VISTA LATERAL do móvel à direita**, mesma escala (profundidade a partir da parede + alturas). NUNCA gerar prancha separada só da lateral. Duas paredes do L continuam lado a lado na mesma prancha.
- **Cotas 2D com as MESMAS cores e texturas do 3D** (madeirado com veio, mármore; chapa 1830 × 2750, veio no comprimento). Cotas em vetor por cima.
- Cadeias de altura por fora das paredes; móvel a mais de 600 mm da parede lateral → cadeia encostada no móvel.

### Regras especiais (só atuam quando o projeto tem esse móvel) — v18, do PDF da Priscila
- **DIVISÓRIA RIPADA** (6+ ripas ≤ 30 × 60–200 mm, ≥ 500 de comprimento, na mesma faixa de profundidade; ex.: ripado com painel de TV no meio do quarto): sai das paredes e vira **bloco próprio** no fim ("MÓDULOS E PAINÉIS – DIVISÓRIA RIPADA" + "MEDIDAS E ALTURAS – DIVISÓRIA RIPADA"). Junta bases, travessas, painel de TV e fechamento na parede. **Listagem: móvel SOZINHO (sem o ambiente), em DUAS pranchas com imagem na DIAGONAL (uma de cada lado do L)**, tabela completa nas duas, **um balão por tipo de peça**. **Cota: TODOS os vãos entre as ripas** (em cada faixa: embaixo, meio, em cima do painel; setas por dentro — o montador precisa da distância entre ripas), largura e altura totais, alturas das partes.
- **DIVISOR DE GAVETA** (joias/talheres: 4+ peças ≤ 18 mm, altura ≤ 100, até 450 mm, nos dois sentidos, encostadas): sai da listagem da parede e ganha **prancha própria "DIVISOR DE GAVETA"**: tabela + **só a vista de cima** (sem 3D da gaveta — não mostrava o divisor; escala até 1:2) com as cotas de todos os vãos e a altura das peças.
- Ainda não feito (ver pendentes): sequência de montagem passo a passo (1º base, 2º laterais… como nas pranchas 12–15 do João) e avisos em amarelo ao montador.

### Planta (prancha 03)
- Só **móveis e paredes** (sem forro, sanca, pedra, eletros por cima). Paredes em peça única desenhadas pelas faces verticais (vãos abertos). Setas das vistas não se sobrepõem.

### Especificações (prancha 03, modelo fixo do João)
- CORES (caixa, portas/frentes, tamponamentos, painéis/tampos, puxadores, portas de vidro) · FERRAGENS (dobradiças, corrediças, puxadores com NOME EXATO do XML, especiais) · ESPESSURAS (caixa + fundo, prateleiras internas, portas/frentes, tamponamentos, painéis/tampos/perfil). Sem item no projeto = em branco. Texto quebra linha, nunca corta.

---

## 4. FONTE DE DADOS (exportação do Promob)

- **Tudo sai do XML + DXF pelo motor.** Os PDFs feitos à mão pelo João são só REFERÊNCIA visual para comparar; nada (cor, medida, imagem) é tirado deles.
- Cor = nome do material no XML → tabela `materiais_cores.json` (ex.: "Metallic Sued" do XML casou com "Metalic Suede" da tabela).

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
- Cota recortada rente ao móvel (paredes somem) e cota pequena no meio da prancha (limite de 75%) → **reprovado** (v15 abre parede a parede e preenche).
- Imagem 3D pequena com margem branca em volta → **reprovado** (v15 preenche o quadro).
- Móvel complexo (ripado) listado no meio do ambiente, de frente → **reprovado** (confuso; faltavam peças). Cota de ripado só com amostra de um vão → **reprovado** (cotar todos os vãos).
- Perder a vista lateral do móvel ao tirar uma parede falsa (v15) → **reprovado**: a lateral agora é da regra das cotas (v16).
- Memória no PC, mexer no PC sem aprovação, versões sem número novo.
- **VETADO**: puxar medida de peça com setinha/chamada no desenho (jeito antigo dos PDFs à mão do João). Medida de peça é SEMPRE pela LISTAGEM (tabela + balões numerados), do jeito que o motor já faz. Ao copiar ideias dos PDFs do João, ignorar as setinhas de medida.

---

## 7. PENDENTE / PRÓXIMO

1. João conferir a **v19** na página (Suíte Casal + 4 projetos) e dizer o que ainda está errado nas imagens → v16.
2. Aprovada → instalar em `C:\CLAUDE\motor v19` (a v13 fica de reserva).
3. Comparar de novo com os cadernos feitos à mão: ângulo de câmera (altura do olho ~1,6 m, perspectiva mais aberta), janela/tomadas/portas do ambiente (só se vierem no DXF), ordem das vistas (João começou pelo armário maior).
4. Cotas da planta (prancha 03) ainda amontoadas.
5. Janela só aparece quando o DXF traz o vão.
6. Sala e Varanda: 2 itens não achados no DXF (Fechamento 70x724x300, Cunha 45° 2700x25x70); vistas C e D com uma peça só (conferir com o João).
7. **AGUARDANDO CONFIRMAÇÃO DO JOÃO (não aplicar antes):** armário em L = uma prancha de cotas dividida AO MEIO, uma parede em cada metade; em cada metade a parte do canto que vai para a outra parede aparece DE LADO (lateral do armário, fechada, cor real) e entra na cadeia de baixo com a largura (ex.: 550 | 520 | 580 e 580 | 620). Referência: PDF do João “Dormitório Casal – Felipe Machado”, prancha 05. Falta o XML+DXF desse projeto (não achado no PC).
8. Onde estão os projetos no PC: `C:\CLAUDE\PROJETO RAFAEL CLARET\<AMBIENTE>` e `C:\CLAUDE\CLIENTES\02_ORIGIN\<CLIENTE>`.
