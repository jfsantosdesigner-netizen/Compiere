# MEMÓRIA OPERACIONAL — MOTOR DE CADERNOS COMPIERE

Atualizado: 25/09/2026 · Substitui qualquer "MEMÓRIA OPERACIONAL" anterior (as antigas estão OBSOLETAS; ignorar). Uma conversa nova começa lendo SÓ este arquivo. Não reler conversas antigas.

## PROTOCOLO DE TRABALHO (João)

- A cada 3 tarefas executadas: atualizar este arquivo → João abre conversa nova → ler só este arquivo → continuar.
- Uma ação por vez, um comando só (script Python via Desktop Commander). Economizar crédito.
- **Usar o PC remoto (Desktop Commander) o MÍNIMO possível.** Consome muitos tokens. Nada de listagens grandes ou buscas amplas (ex.: `findstr` em JSON gigante). Ler só o arquivo necessário.
- Não perguntar o que já tem regra. Cruzar dados sozinho. Trazer resultado pronto.
- Sede: `C:\CLAUDE`. Drive: só leitura. PC: Desktop Commander, device JOAO-FELIPE.
- **Memória fica SÓ no Claude**, no repositório da nuvem (`Compiere/MEMORIA_OPERACIONAL.md` + PDF). **Nunca gravar memória no PC.** O PC serve só para o motor e para operações.
- **VERSÕES (regra do João):** cada rodada de correções = NOVA VERSÃO (VERSAO.txt + ramo `vN` no GitHub; tags são bloqueadas pela conexão, por isso ramos). Nunca deixar versão para trás: ramos `v9`, `v10`, `v11` guardados. **Atual: v14 na nuvem (aguardando aprovação); v13 instalada no PC (`C:\CLAUDE\motor v13`, Pillow+numpy OK); v10 reserva.** Próxima rodada = v15. Ramos guardados: v9…v13.
- Versão do motor = nome da pasta. **PC: `C:\CLAUDE\motor v10`** = clone git do repositório `motor-cadernos-compiere` (o PC tem acesso ao GitHub). Atualizar o PC = `git pull` nessa pasta (1 comando, nenhum arquivo passa pelo Claude). Nova versão grande → novo clone em `motor vN` + caminhos do `padrao.json`. `motor v9` ficou como reserva.

## REGRAS FIXAS DO CADERNO (definitivas: não mudar, não perguntar)

1. Sequência: Capa → Contrato → Planta+Especificações → Visão Geral → por vista: Listagem, Cotas. **UMA LETRA POR PAREDE** (A, B, C, D…; em cada L, a parede maior primeiro). LISTAGEM sempre FRONTAL e POR PAREDE, listando SÓ os móveis daquela parede (3D diagonal foi testado e REPROVADO: paredes na frente dos móveis). Parede **< 2,5 m**: as COTAS vão lado a lado com a vizinha do L (mesma escala, colunas proporcionais). Ordem: Listagem A → Listagem B → Cotas A|B → Listagem C → … Pranchas = 4 + nº paredes + nº blocos de cotas. Nicho pequeno/apertado ganha imagem de DETALHE embaixo da tabela (continua na imagem grande).
2. LISTAGEM: 3D FRONTAL (câmera na FRENTE dos móveis, nunca nas costas), PORTAS FECHADAS, com paredes, balões amarelos. Tabela Item | Descrição | Dimensão. Lista só módulos, tamponamentos e fechamentos. Sem cotas.
3. COTAS: 2D FRONTAL, PORTAS ABERTAS, com paredes (só como referência). Cotar só módulos inteiros + alturas de prateleiras. Nada externo (janela, piso, eletro).
4. ESPECIFICAÇÕES (prancha 03): cores (caixa, portas, tamponamentos) + FERRAGENS (dobradiças, corrediças, puxadores, portas de alumínio/vidros/espelhos) + espessuras. Ferragens só nessa prancha.
5. **AMBIENTE EM VOLTA**: a imagem 3D da listagem e o 2D das cotas mostram o ambiente (móveis vizinhos, pedra) para orientar; listagem, balões e cotas SÓ dos móveis da parede da vista. Pedra/eletros/janela = referência, NUNCA cotados. Pedra só aparece nas vistas onde ela está. Paredes: as REAIS do DXF que compõem o L (fundo e laterais inteiras, com janela/vão); tira só a que fica na frente. Nicho com imagem de detalhe: balões SÓ no detalhe, não na imagem grande. Cotas de altura a partir do piso pronto.
6. Imagens limpas: peças desenhadas como caixas, só bordas, sem triangulação. **Só MDF** (sem suportes, dobradiças, cabideiros, pés). Nada atravessa portas/rodapé.
7. Escala mínima 1:25. A4 paisagem, nada encosta no quadro.
8. Fonte de dados: XML MONTADO + DXF exportados do Promob. DXF tem de vir com **uma camada por peça** (o de 16:02 serve; o de 16:11 veio agrupado por cor e NÃO serve). Janela e eletros ainda não vieram no DXF. Explodido = só Produção Nadecor. SketchUp/3DS não são usados.

## MOTOR (pronto para o João usar sem IA)

- Pasta: `C:\CLAUDE\motor v8\`. Arquivos: `gerar_caderno.py` (principal), `geo.py` (liga XML↔DXF), `motor_caderno.py`, `motor_lista.py`, `dxf_pecas.py`, `novo_ambiente.py`, `GERAR_CADERNO.bat`, `padrao.json`, `materiais_index.json`, `assets\LAYOUT_FIXO.pdf`, `assets\CONTRATO.pdf`, `assets\LOGO.png`.
- Caminhos internos já apontam para `motor v8` (`padrao.json`: contrato_fonte + logo; `config_cozinha_v2.json` e `config_escritorio.json`: pecas_json). Conferido em 25/09/2026.
- Histórico (VERSAO.txt):
  - **v8**: cores reais (XML → pasta `C:\CLAUDE\MATERIAIS`, índice em `materiais_index.json`) + capa nova (logo trocável em `padrao.json`).
  - **v7**: listagem 3D frontal com portas fechadas e paredes | cotas 2D frontal com portas abertas | ferragens só na P03 | imagens limpas | escala mín. 1:25.
- Uso: pasta do ambiente dentro da pasta do cliente (ex.: `PROJETO FULANO\COZINHA`) com XML montado + DXF → arrastar a pasta no `GERAR_CADERNO.bat` → sai `CADERNO - <AMBIENTE>.pdf` + `_QUALIDADE.md` na pasta.
- Cliente = nome da pasta-mãe sem "PROJETO"; ambiente = nome da pasta; projetista/arquiteta em `padrao.json` ou em `dados.json` na pasta do cliente.
- Se o PDF estiver aberto no leitor, o motor salva com sufixo de hora (não trava).
- 3D ativo = função `render3d(page, rect, pids, letra=None, **kw)` (perspectiva; paredes/piso desenhados primeiro, móveis peça por peça do fundo para a frente). Versões antigas foram renomeadas para `_render3d_old*`.

## CORREÇÕES JÁ FEITAS (não refazer)

- Planta: só móveis e paredes (sem forro/sanca/pedra/eletros); setas das vistas não se sobrepõem.
- TODO nicho aberto (3+ painéis/tamponamentos, 2+ horizontais, até 2 m × 1,2 m; peças "Vista" fora) = DETALHE embaixo da tabela, balões só lá; vários detalhes lado a lado.
- **NICHO = estrutura ABERTA, SEM PORTA** (sem porta/basculante/gaveta), com ou sem prateleira. Armário COM PORTA NUNCA é nicho (nem em cima da geladeira). Porta = chapa fina na frente cobrindo ≥ 40% do módulo (geometria do DXF). Módulo aberto (até 2 m × 1,2 m) + tamponamentos = DETALHE; grupos encostados = um detalhe. Nicho > 2 m fica na imagem principal.
- Item escondido atrás dos módulos (ex.: painel nas costas da ilha) = DETALHE - COSTAS visto de trás.
- Cotas: parede/móvel pequeno amplia até 1:20 ou 1:15 (ocupando até 75% do espaço).
- Paredes: planta pelas faces verticais das paredes; 3D sem parede na frente do fundo dos móveis; móvel ALTO sem parede real atrás ganha parede de fundo de referência; ilha/bancada baixa não. Rodapé solto no chão não é parede/eletro. SEMPRE regerar os 4 projetos a cada versão.
- Desenho vetorial: traço de arestas SEMPRE com closePath=False (senão aparecem diagonais da triangulação). Só arestas retas são contorno.
- Listagem BEM FRONTAL (câmera 3°). Contornos nítidos de paredes/janela/pedra (arestas reais, sem triangulação). Blocos QUADRADOS de eletro (12 faces) NÃO entram; fica objeto com forma real; em cima da pedra só cuba/cooktop (até 300 mm).
- Textura = CHAPA 1830 × 2750 mm (veio nos 2750); cada peça usa o pedaço proporcional. Texturas 1024 px.
- TEXTURA REAL (veio da madeira) no 3D: 3D vira imagem 170 dpi com a textura do material em cada face; texturas em `texturas/` (512 px). Precisa Pillow + numpy no PC (sem eles, cor lisa).

- Mesma parede com módulos de profundidades diferentes (planos até 600 mm) = uma vista só.
- DXF com todas as paredes numa peça só: motor usa as faces reais (não a caixa).
- Eletros/objetos do ambiente (geladeira, micro, forno...) = referência cinza, sem cota. Eletro = volume (menor medida ≥ 40 mm), não confundir com porta solta.

- Listagem por quantidade do XML (peças repetidas de painel/tamponamento).
- "Rodapé" na descrição não vira componente (`re.match` no início da descrição); módulos com rodapé são aceitos.
- Cor da caixa buscada nos subitens (lateral/base); espessura da caixa pelas laterais (15–30 mm).
- Laje/piso fora da planta; paredes em linha preta simples; seta de vista na planta.
- v8: cores reais dos materiais + capa nova com logo.

## RESULTADOS

- Escritório Rafael Claret: `C:\CLAUDE\PROJETO RAFAEL CLARET\ESCRITÓRIO\CADERNO - ESCRITÓRIO.pdf` (gerado pelo motor v7): 6 pranchas, 7/7 itens, XML confere, tudo APROVADO. Uma vista só (não existe vista B). Falta regerar na v8.
- Cozinha Caroline (CLIENTES\\02_ORIGIN\\CAROLINE\\COZINHA): 8 pranchas, 38/38, parede linear + parede com despenseiro/península; exemplo em `exemplos/CAROLINE_COZINHA`.
- Cozinha Felipe (CLIENTES\\02_ORIGIN\\FELIPE\\COZINHA): 8 pranchas, 30/30, parede linear + ilha; exemplo em `exemplos/FELIPE_COZINHA`.
- Cozinha Rafael Claret: 8 pranchas, 40/41 itens (o Painel Freijó 719x18x364 não foi localizado no DXF).

## MOTOR NA NUVEM (desde 25/09/2026)

- Repositório GitHub: `jfsantosdesigner-netizen/motor-cadernos-compiere` (ramo `main`). v14 no GitHub (ramo `main` = ramo `v14`); PC em `C:\CLAUDE\motor v13`. Ao aprovar: clonar ramo v14 em `C:\CLAUDE\motor v14`. Ao aprovar: clonar o ramo aprovado em `C:\CLAUDE\motor vN` (a anterior fica como reserva) + conferir Pillow/numpy.
- Visualizar sem baixar: página privada https://claude.ai/artifact/XBbud5f2JXjymBFaGjdcYn (gerada por `ferramentas/visualizador.py`, republicar no mesmo link).
- Trabalho: trazer do PC só XML montado + DXF (zip em base64, 1 comando), gerar e corrigir na nuvem. Exemplos em `exemplos/ESCRITORIO` e `exemplos/COZINHA2`.
- v10: só MDF no 3D/2D; 3D ordenado por peça; cor de peças de mesma medida pela ordem XML×DXF (DXF = XML invertido); cotas internas; prancha 03 completa; uma vista por parede.
- Cores reais: **FEITO**. `materiais_cores.json` (12.971 texturas, gerado no PC por `C:\CLAUDE\ferramentas\gerar_cores_materiais.py`) está no repositório; o motor não precisa da pasta MATERIAIS de 3 GB. Testado: Pecan, Freijó Puro, Mogno Imperial, Nero, Branco, Chumbo, Preto TX.

## PENDENTE / PRÓXIMO

0. João vai atualizar XML + DXF da `COZINHA 2` (com pedra, eletros, janela) → trazer e regerar; cotas devem mostrar janela/pedra/eletros como referência (ver prancha 05 do caderno aprovado). João conferir Cozinha 2 e Escritório na v10. Pontos vistos: cotas da planta (prancha 03) amontoadas; Painel Freijó 719x18x364 não está no DXF.
1. João testar a v13 no PC (arrastar a pasta do ambiente no `GERAR_CADERNO.bat` de `C:\CLAUDE\motor v13`). Próximas versões: só ir ao PC depois de aprovar (`git pull` em `C:\CLAUDE\motor v10` + `pip install pillow numpy` se faltar). NÃO mexer no PC sem aprovação.
2. Cotas da planta (prancha 03) amontoadas.
3. Janela ainda não vem no DXF.
3. Testar em um 3º projeto novo (cliente novo) para validar que o motor generaliza.
4. Depois: cadernos Nadecor (Produção peça a peça, Instalação).
