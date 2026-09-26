# MEMÓRIA OPERACIONAL — MOTOR DE CADERNOS COMPIERE

**Reescrita do zero em 25/09/2026; atualizada na v26.** Este arquivo é a ÚNICA fonte. Ignore qualquer memória ou conversa anterior. Só está aqui o que foi testado e aprovado.

---

## 1. ONDE ESTAMOS (resumo)

| Item | Situação |
|---|---|
| Motor no PC | **v26** em `C:\CLAUDE\motor v26` (instalada 25/09 a pedido do João, copiada de `Compiere/motor v26`; usa `C:\CLAUDE\MATERIAIS` direto). `motor v25`, `v24`, `v23`, `v13` = reserva. |
| Motor na nuvem | **v26 COMPLETA guardada no repositório Compiere, pasta `motor v26/`** (ramo `claude/pensive-hopper-rbahkx`) — o repositório do motor recusou o envio (só leitura nesta sessão). No motor: `main` = `v25` (intacta). Próxima sessão com acesso push: criar ramo `v26` no motor a partir dessa pasta. |
| Versões guardadas | Ramos `v9` … `v25` no GitHub (v26 pendente de envio) (tags são bloqueadas pela conexão; por isso ramos). |
| Ver cadernos sem baixar | Página privada: https://claude.ai/artifact/XBbud5f2JXjymBFaGjdcYn (9 abas, Priscila Cozinha primeiro, versão v26; republicar no mesmo link com `ferramentas/visualizador.py`). |
| Projetos de teste | Caroline Cozinha (8 pr., 38/38) · Felipe Cozinha (8 pr., 30/30) · Rafael Cozinha 2 (10 pr., 41/41) · Rafael Escritório (6 pr., 7/7, agora com o DXF) · Rafael Suíte Casal (10 pr., 12/12) · Rafael Sala e Varanda (11 pr., 16/18) · Rafael Área de Serviço (6 pr., 10/10) · Priscila Suíte Casal – DESAFIO (18 pr. na v22, 61/63; PDF do João = referência das regras especiais; `C:\CLAUDE\CLIENTES\02_ORIGIN\PRISCILA\SUITE CASAL`). **Priscila Cozinha (v26, 13 pr., 51/53; PDF do João = referência; `C:\CLAUDE\CLIENTES\02_ORIGIN\PRISCILA\cozinha`)**. Todos em `exemplos/` no repositório (a Priscila Cozinha só no commit local da v26). |
| Próximo | João conferir a Priscila Cozinha v26 na página. Enviar a v26 ao GitHub (precisa acesso push). Puxadores: descobrir como exportar do Promob. |
| Referência | Cadernos feitos À MÃO pelo João (modelo das imagens): Suíte Casal, Caroline, Felipe, Cozinha 2 (Área de Serviço), Escritório — comparar sempre as imagens do motor com eles. |

---

## 2. PROTOCOLO DE TRABALHO (obrigatório)

0. **Gastar pouco: não ficar girando. NUNCA alterar a versão anterior — sempre criar versão nova completa (pasta/ramo). Se o GitHub do motor recusar, guardar a versão completa no repositório Compiere (`motor vN/`).**

1. **PC remoto (Desktop Commander, device JOAO-FELIPE) o MÍNIMO possível** — gasta muitos tokens. Um comando por vez, só para: trazer XML + DXF (zip em base64 num comando só), trazer texturas (só leitura), instalar versão aprovada.
2. **Todo o trabalho é na nuvem**, no repositório do motor. Gerar e conferir lá.
3. **Nada vai para o PC sem o João aprovar.** Instalação = `git clone --depth 1 -b vN` em `C:\CLAUDE\motor vN` (a anterior fica de reserva) + conferir Pillow/numpy.
4. **Toda correção é REGRA do motor**, nunca ajuste só para um projeto. **O motor é REGRAS + CONDIÇÕES**: o que está certo NÃO se apaga; cada situação nova (projeto novo) vira uma CONDIÇÃO nova que só atua quando aparece. Sempre regerar todos os projetos e conferir que os que não têm a situação não mudaram.
5. **Cada rodada de correções = nova versão**: atualizar `VERSAO.txt`, caminhos do `padrao.json` (`motor vN`), commit, ramo `vN` no GitHub. Próxima = **v27**.
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
- ~~Parede sozinha na prancha de cotas → frontal + lateral~~ **SUBSTITUÍDA na v26: cota só frontal, sem lateral.** Duas paredes do L continuam lado a lado na mesma prancha.
- **Cotas 2D com as MESMAS cores e texturas do 3D** (madeirado com veio, mármore; chapa 1830 × 2750, veio no comprimento). Cotas em vetor por cima.
- Cadeias de altura por fora das paredes; móvel a mais de 600 mm da parede lateral → cadeia encostada no móvel.

### Regras especiais (só atuam quando o projeto tem esse móvel) — v18, do PDF da Priscila
- **DIVISÓRIA RIPADA** (6+ ripas ≤ 30 × 60–200 mm, ≥ 500 de comprimento, na mesma faixa de profundidade; ex.: ripado com painel de TV no meio do quarto): sai das paredes e vira **bloco próprio** no fim ("MÓDULOS E PAINÉIS – DIVISÓRIA RIPADA" + "MEDIDAS E ALTURAS – DIVISÓRIA RIPADA"). Junta bases, travessas, painel de TV e fechamento na parede. **Listagem: móvel SOZINHO (sem o ambiente), em DUAS pranchas: 3D FRONTAL (todas as ripas, como a cota) e 3D LATERAL RETA (90°) pelo lado da perna do L** (mostra as ripas do L; nunca diagonal). **A prancha da lateral lista SÓ as peças que APARECEM nela** (buffer de visibilidade: 15%+ da peça à vista), numeração própria, tabela completa nas duas, **um balão por tipo de peça**. **Cota: TODOS os vãos entre as ripas** (em cada faixa: embaixo, meio, em cima do painel; setas por dentro — o montador precisa da distância entre ripas), largura e altura totais, alturas das partes.
- **DIVISOR DE GAVETA** (joias/talheres: 4+ peças ≤ 18 mm, altura ≤ 100, até 450 mm, nos dois sentidos, encostadas): sai da listagem da parede e ganha **prancha própria "DIVISOR DE GAVETA"**: tabela + **3D SÓ das peças do divisor (isolado) com balões** + **vista de cima** com cotas (escala até 1:2). Nunca 3D da gaveta inteira (não mostra o divisor). com as cotas de todos os vãos e a altura das peças.
- **GAVETA / MÓDULO MONTADO COM PAINÉIS** (não é módulo do Promob: fundo horizontal ≥ 0,1 m² acima de 300 mm + 3+ peças em pé do mesmo material, até 140 mm acima do fundo; ex.: gaveta da penteadeira): sai da listagem da parede → **prancha própria "GAVETA MONTADA COM PAINÉIS"** (tabela + 3D isolado com balões + vista de cima com cotas). Deixa a vista frontal da parede limpa.
- **CONDIÇÃO "LISTAGEM POLUÍDA"** (parede com 12+ peças numeradas; não vale para a divisória): imagem grande só com os painéis/móveis principais. **Módulo pequeno fechado e SOLTO** (até 1 m × 0,7 m, com porta/gaveta, sem módulo encostado; ex.: mesa de cabeceira suspensa) + tampo → **detalhe embaixo da tabela** com o nome do módulo (um por tipo), balões só lá. **Peça escondida atrás de painel** (afastadores atrás da cabeceira) → **detalhe das costas**. O relatório avisa quando dispara. (Disparou em: Priscila Vista C, Sala Vista A, Caroline Vista A.)
- **CONDIÇÃO "PERNA DO L"** (planta do João: TODO trecho com móvel tem VISTA): peças de uma parede que vão > 300 mm além da frente dos módulos, num trecho de 600 mm+ (ex.: penteadeira em L) → vista própria, olhada pelo lado de dentro do L, logo DEPOIS da vista da parede dela (b → c).
- **CONDIÇÃO "RODAPÉ / BASE ESCONDIDA"**: 3+ peças até 150 mm do piso, com uma no sentido da profundidade (quadro de base embaixo do móvel) → **detalhe "RODAPÉ / BASE"** embaixo da tabela (3D de cima em diagonal), balões só lá.
- **(v26, cozinha Priscila) CONDIÇÃO "PAREDE CORTADA POR PILAR / VÃO"**: móveis da mesma parede dos dois lados de uma parede real que atravessa a faixa dos móveis (pilar, verga de vão de passagem; cada lado com 1 m+ de módulos) = DUAS vistas (listagem e cotas próprias; escala maior). O que fica atrás do plano da vista não aparece (só nessas vistas e no bloco).
- **(v26) CONDIÇÃO "CONJUNTO DE PAINÉIS SEM MÓDULO"**: paredes só com painéis que se encostam (painel com nichos na ponta da parede, painel do teto, agastadores) = BLOCO PRÓPRIO no fim, "PAINEL COM NICHOS" (como a divisória: 3D frontal + 3D lateral reta, móvel sozinho, um balão por tipo; cota frontal com os vãos usinados e alturas do piso + lateral com profundidade do painel do teto; elevação curta em volta, escala maior).
- **(v26) CONDIÇÃO "PAINEL USINADO"**: painel em pé na frente de estrutura de nichos aberta (2 laterais + 3+ prateleiras até 150 mm atrás) = painel desenhado com os VÃOS alinhados aos nichos (o DXF traz o painel inteiro). Balão na faixa cheia.
- **(v26) DIVISOR DE TALHER** (cozinha): mesma regra do divisor de gaveta, peças até 750 mm, conjunto até 800 × 800, peças deitadas (altura ≤ 100 no DXF).
- **(v26) MÓDULO BAIXO / GIRADO** (adega 150 × 870 × 600 do Promob = 870 de largura, 150 de altura): achado (laterais de 100–150 mm só para módulo ≤ 200 mm).
- **(v26)** Porta avulsa do XML (ID `POR_...`) = porta, não entra na listagem. Peça do DXF fora do XML duplicada no lugar de uma peça listada não é desenhada. Detalhe de NICHO não leva painel alto (até o teto) encostado.
- **Barrote / Cunha 45° NÃO faz parte (João, v26)**: lista só material. Não tentar casar barrote. A Cunha sai da listagem.
- **(v26, João) LISTAGEM POLUÍDA (mais de 15 linhas) = DUAS pranchas**: SUPERIORES (armários de cima e altos) e INFERIORES (balcões); sem os dois grupos, PARTE 1 / PARTE 2. Tabela, balões e detalhes só de cada parte.
- **(v26, João) COTA É SÓ A VISTA FRONTAL** — a prancha de cotas NÃO tem vista lateral (substitui a regra da v16).
- Ainda não feito (ver pendentes): sequência de montagem passo a passo (1º base, 2º laterais… como nas pranchas 12–15 do João) e avisos em amarelo ao montador.

### Planta (prancha 03)
- **Regra geral (v23): UMA cota por parede = COMPRIMENTO TOTAL dos móveis** (planta limpa, como a do João). Nunca cotar peça por peça.
- Só **móveis e paredes** (sem forro, sanca, pedra, eletros por cima). Paredes em peça única desenhadas pelas faces verticais (vãos abertos). Setas das vistas não se sobrepõem.

### Especificações (prancha 03, modelo fixo do João)
- CORES (caixa, portas/frentes, tamponamentos, painéis/tampos, puxadores, portas de vidro) · FERRAGENS (dobradiças, corrediças, puxadores com NOME EXATO do XML, especiais) · ESPESSURAS (caixa + fundo, prateleiras internas, portas/frentes, tamponamentos, painéis/tampos/perfil). Sem item no projeto = em branco. Texto quebra linha, nunca corta.

---

## 4. FONTE DE DADOS (exportação do Promob)

- **PROIBIDO pegar qualquer imagem ou conteúdo dos PDFs/cadernos executivos do João para gerar o caderno. O motor gera TUDO sozinho (XML + DXF). Nunca mexer nos cadernos executivos dele.** Os PDFs dele servem só para ler ideias de regra.
- **Materiais**: o motor procura sozinho: 1º `C:\CLAUDE\motor vN\MATERIAIS` (se existir), 2º `C:\CLAUDE\MATERIAIS` (original). **Hoje usa direto a original `C:\CLAUDE\MATERIAIS`** — não copiar para dentro do motor (João, 25/09). Cores vêm de `materiais_cores.json` (não dependem da pasta); a pasta só dá a textura com veio.
- **Redução de acervos ADIADA (João: "depois a gente pensa")**: ferramenta pronta `ferramentas/reduzir_acervo.py materiais|promob` (MATERIAIS 3,1 GB → texturas 512 px; bibliotecas do Promob ~4 GB, 158 mil arquivos → imagens 256 px + 400 .obj (64 de puxadores) + `indice.json`; .PMOB/.MOB3D/.entity são binários do Promob, não usáveis). Não rodar sem o João pedir.
- **Puxadores NÃO vêm no DXF** (conferido em 25/09: só faces/malhas das peças; as plaquinhas 13×26 atrás das portas são dobradiças). Regra que gerava o puxador pelo lado oposto às dobradiças ficou DESLIGADA (João: posições erradas).

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

## 4b. COMO TRAZER ARQUIVOS DO PC (testado na v26)

- Um comando `python -c` no PC (cmd) que compacta em `%TEMP%` (XML+DXF em `.tar.xz`, 33 MB → 1,1 MB; PDF de referência em JPG 90 dpi) e outro que imprime o base64. A saída grande é SALVA SOZINHA num arquivo `tool-results/*.txt` na nuvem → extrair com python (regex do maior bloco base64). Depois apagar os arquivos do `%TEMP%`.
- No PowerShell via Desktop Commander o `$` some: usar `shell: cmd`.

## 6. NÃO FAZER (testado e reprovado / substituído)

- **SETAS com nome e medida escritos na imagem → VETADO pelo João.** Identificação é SEMPRE por LISTA (tabela) + balões numerados. Não propor de novo.

- 3D na diagonal pegando duas paredes na listagem (paredes na frente dos móveis) → **reprovado**.
- "Nicho suspenso" (armário sobre geladeira vira detalhe mesmo com porta) → **errado**, substituído pela definição de nicho aberto.
- Caixa (bbox) de parede em peça única → cobria tudo; usar faces reais.
- Blocos quadrados de eletro na imagem → poluem; fora.
- Cota recortada rente ao móvel (paredes somem) e cota pequena no meio da prancha (limite de 75%) → **reprovado** (v15 abre parede a parede e preenche).
- Imagem 3D pequena com margem branca em volta → **reprovado** (v15 preenche o quadro).
- Móvel complexo (ripado) listado no meio do ambiente, de frente → **reprovado** (confuso; faltavam peças). Cota de ripado só com amostra de um vão → **reprovado** (cotar todos os vãos). Ripado em 3D na diagonal (±38° ou 62°) → **reprovado** (confuso; usar frontal + lateral RETA do L).
- Perder a vista lateral do móvel ao tirar uma parede falsa (v15) → **reprovado**: a lateral agora é da regra das cotas (v16).
- Memória no PC, mexer no PC sem aprovação, versões sem número novo.
- **VETADO**: puxar medida de peça com setinha/chamada no desenho (jeito antigo dos PDFs à mão do João). Medida de peça é SEMPRE pela LISTAGEM (tabela + balões numerados), do jeito que o motor já faz. Ao copiar ideias dos PDFs do João, ignorar as setinhas de medida.

---

## 7. PENDENTE / PRÓXIMO

1. **v26 está em `Compiere/motor v26/` (completa).** Criar o ramo `v26` no repositório do motor quando houver acesso push. **NUNCA alterar a versão anterior: cada versão é pasta/ramo NOVO e completo (João).**
2. João conferir a **Priscila Cozinha v26** na página. Comparado com o PDF dele: FEITO = ilha (painel com nichos) em bloco, divisor de talher, adega, parede da pia dividida (cozinha / lado da churrasqueira). FALTA: sequência de montagem passo a passo (pranchas 05–08 e 12–14 dele), avisos em amarelo ao montador (LED, interruptor, "cliente instala spot"), listagem dividida superiores/inferiores (pranchas 04 e 08 dele), metalon (DXF só traz uma barra) e esquema elétrico (não vem no XML/DXF).
3. Instalar no PC só depois da aprovação (`C:\CLAUDE\motor v26`; v25 fica de reserva).
4. Comparar de novo com os cadernos feitos à mão: ângulo de câmera (olho ~1,6 m), janela/tomadas/portas (só se vierem no DXF), ordem das vistas.
5. Janela só aparece quando o DXF traz o vão.
6. Sala e Varanda: Fechamento 70x724x300 e Cunha 45° não achados no DXF (Cunha = barrote, não faz parte); vistas C e D com uma peça só (conferir com o João).
7. **AGUARDANDO CONFIRMAÇÃO DO JOÃO (não aplicar antes):** armário em L = uma prancha de cotas dividida AO MEIO, uma parede em cada metade; em cada metade a parte do canto que vai para a outra parede aparece DE LADO (lateral do armário, fechada, cor real) e entra na cadeia de baixo com a largura (ex.: 550 | 520 | 580 e 580 | 620). Referência: PDF do João “Dormitório Casal – Felipe Machado”, prancha 05. Falta o XML+DXF desse projeto (não achado no PC).
8. Onde estão os projetos no PC: `C:\CLAUDE\PROJETO RAFAEL CLARET\<AMBIENTE>` e `C:\CLAUDE\CLIENTES\02_ORIGIN\<CLIENTE>`.
9. Suíte Priscila na v26: a "Frente de Gaveta Reta 406x130x18" (não achada no DXF) saiu da listagem pela regra da porta avulsa — confirmar com o João.


## v27 (26/09/2026) — REGRA GERAL: TUDO QUE ESTÁ NA LISTA APARECE NÍTIDO
- Peça listada que NÃO aparece na imagem principal (escondida embaixo/atrás/entre módulos) ou balões AMONTOADOS (3+ a até 22 pt) → sai da imagem principal e vai para SUB-IMAGEM "COMO FICA MONTADO" (só a peça + móveis encostados, sem ambiente; vista de baixo se estiver no alto).
- UMA sub-imagem por prancha: a prancha é REPLICADA ("… – DETALHE n"), 3D principal ao lado. Sem limite de pranchas.
- Leitura guardada do DXF confere hash (DXF mudou → lê de novo). Removido o modo antigo que puxava listagem/imagens de PDF.
- A outra conversa (v26) foi PARADA pelo João (se perdeu). Esta memória + ramo v27 do motor são a referência. Próxima = v28.

## v28 (26/09/2026) — 25 COMENTÁRIOS DO JOÃO NA PÁGINA (viraram regras gerais)
- SUB-IMAGEM: peça no alto = vista DE CIMA para baixo; peça embaixo = de baixo; só os MÓDULOS onde a peça está; SEM PORTAS (mostra o que tem dentro, ex.: cantoneira). Amontoado = 3+ balões a até 16 pt.
- Peça suspensa sob tampo (gaveta de teclado) e módulo de CANTO ganham sub-imagem. UM detalhe por prancha (prancha replicada "– DETALHE n").
- "Costas atrás de painel" (v21) trocado pela regra geral de peça escondida (v27).
- "Parede" com até 2 peças encostadas em móvel de outra parede junta nela (Sala C/D resolvido).
- VISÃO GERAL: mais de 4 vistas = uma imagem diagonal para cada 2 vistas.
- Móvel feito com GEOMETRIA (DXF sem XML) encostado em móvel = referência na imagem, igual à pedra (sem lista/cota). "Gôndola" era erro de leitura: é GEOMETRIA.
- Divisor/gaveta de painéis: imagem pequena "ONDE FICA". Painel com nichos: 2ª imagem na diagonal; ripas centrais listadas na lateral da divisória.
- PLANTA: cota de CADA CONJUNTO de móveis (comprimento + largura), sem cotar o vão entre conjuntos.
- NÃO DÁ pelos dados: Frente de Gaveta Reta 406x130x18 e Gaveta Corrediça Telescópica não vêm no DXF.
- Página: dpi 95 (limite 16 MB). Ramo v28 do motor. PC: v28 INSTALADA em C:\CLAUDE\motor v28 (testada, Felipe APROVADO); versões antigas APAGADAS a pedido do João; resto do C:\CLAUDE o João limpa. Próxima = v29.

## v29 (26/09/2026) — ERROS DA v28 NO PROJETO REAL (Guilherme Cesar)
- v28 reprovada pelo João em projeto real: (1) regra "geometria" pegava PORTAS do XML e pintava de cinza por cima; (2) sarrafos atrás da cabeceira em sub-imagem errada (painel tampando / junto do criado-mudo).
- v29: peça com medida+cor do XML nunca é geometria; VOLTA o DETALHE - COSTAS da v21 (peça atrás de painel), sempre.
- LIÇÃO: testar versão nova também em PROJETO REAL novo, não só nos 9 de teste.
- PC: motor v25, v26, v27, v28 e v29 em C:\CLAUDE. Cadernos Guilherme gerados no PC pela v29 (… v29.pdf nas pastas dele no Desktop).
