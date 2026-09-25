# MEMÓRIA OPERACIONAL — MOTOR DE CADERNOS COMPIERE

Atualizado: 25/09/2026 · Substitui qualquer "MEMÓRIA OPERACIONAL" anterior (as antigas estão OBSOLETAS; ignorar). Uma conversa nova começa lendo SÓ este arquivo. Não reler conversas antigas.

## PROTOCOLO DE TRABALHO (João)

- A cada 3 tarefas executadas: atualizar este arquivo → João abre conversa nova → ler só este arquivo → continuar.
- Uma ação por vez, um comando só (script Python via Desktop Commander). Economizar crédito.
- **Usar o PC remoto (Desktop Commander) o MÍNIMO possível.** Consome muitos tokens. Nada de listagens grandes ou buscas amplas (ex.: `findstr` em JSON gigante). Ler só o arquivo necessário.
- Não perguntar o que já tem regra. Cruzar dados sozinho. Trazer resultado pronto.
- Sede: `C:\CLAUDE`. Drive: só leitura. PC: Desktop Commander, device JOAO-FELIPE.
- **Memória fica SÓ no Claude**, no repositório da nuvem (`Compiere/MEMORIA_OPERACIONAL.md` + PDF). **Nunca gravar memória no PC.** O PC serve só para o motor e para operações.
- Versão do motor = nome da pasta (**atual: `C:\CLAUDE\motor v8`**, com VERSAO.txt). Nova versão → renomear a pasta (próxima: `motor v9`) e atualizar os caminhos internos (`padrao.json`, `config_cozinha_v2.json`, `config_escritorio.json`) e o VERSAO.txt.

## REGRAS FIXAS DO CADERNO (definitivas: não mudar, não perguntar)

1. Sequência: Capa → Contrato → Planta+Especificações → Visão Geral → por vista: Listagem, Cotas. **UMA LETRA POR PAREDE** (A, B, C, D…; em cada L, a parede maior primeiro). LISTAGEM sempre FRONTAL e POR PAREDE, listando SÓ os móveis daquela parede (3D diagonal foi testado e REPROVADO: paredes na frente dos móveis). Parede **< 2,5 m**: as COTAS vão lado a lado com a vizinha do L (mesma escala, colunas proporcionais). Ordem: Listagem A → Listagem B → Cotas A|B → Listagem C → … Pranchas = 4 + nº paredes + nº blocos de cotas. Nicho pequeno/apertado ganha imagem de DETALHE embaixo da tabela (continua na imagem grande).
2. LISTAGEM: 3D FRONTAL (câmera na FRENTE dos móveis, nunca nas costas), PORTAS FECHADAS, com paredes, balões amarelos. Tabela Item | Descrição | Dimensão. Lista só módulos, tamponamentos e fechamentos. Sem cotas.
3. COTAS: 2D FRONTAL, PORTAS ABERTAS, com paredes (só como referência). Cotar só módulos inteiros + alturas de prateleiras. Nada externo (janela, piso, eletro).
4. ESPECIFICAÇÕES (prancha 03): cores (caixa, portas, tamponamentos) + FERRAGENS (dobradiças, corrediças, puxadores, portas de alumínio/vidros/espelhos) + espessuras. Ferragens só nessa prancha.
5. **AMBIENTE EM VOLTA**: a imagem 3D da listagem e o 2D das cotas mostram o ambiente (móveis vizinhos, pedra) para orientar; listagem, balões e cotas SÓ dos móveis da parede da vista. Pedra/eletros/janela = referência, NUNCA cotados. Pedra só aparece nas vistas onde ela está. Cotas de altura a partir do piso pronto.
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

- Listagem por quantidade do XML (peças repetidas de painel/tamponamento).
- "Rodapé" na descrição não vira componente (`re.match` no início da descrição); módulos com rodapé são aceitos.
- Cor da caixa buscada nos subitens (lateral/base); espessura da caixa pelas laterais (15–30 mm).
- Laje/piso fora da planta; paredes em linha preta simples; seta de vista na planta.
- v8: cores reais dos materiais + capa nova com logo.

## RESULTADOS

- Escritório Rafael Claret: `C:\CLAUDE\PROJETO RAFAEL CLARET\ESCRITÓRIO\CADERNO - ESCRITÓRIO.pdf` (gerado pelo motor v7): 6 pranchas, 7/7 itens, XML confere, tudo APROVADO. Uma vista só (não existe vista B). Falta regerar na v8.
- Cozinha Rafael Claret: 8 pranchas, 40/41 itens (o Painel Freijó 719x18x364 não foi localizado no DXF).

## MOTOR NA NUVEM (desde 25/09/2026)

- Repositório GitHub: `jfsantosdesigner-netizen/motor-cadernos-compiere` (ramo `main`). Versão atual lá: **v10**. PC ainda em `motor v9`.
- Visualizar sem baixar: página privada https://claude.ai/artifact/XBbud5f2JXjymBFaGjdcYn (gerada por `ferramentas/visualizador.py`, republicar no mesmo link).
- Trabalho: trazer do PC só XML montado + DXF (zip em base64, 1 comando), gerar e corrigir na nuvem. Exemplos em `exemplos/ESCRITORIO` e `exemplos/COZINHA2`.
- v10: só MDF no 3D/2D; 3D ordenado por peça; cor de peças de mesma medida pela ordem XML×DXF (DXF = XML invertido); cotas internas; prancha 03 completa; uma vista por parede.
- Cores reais: `C:\CLAUDE\ferramentas\gerar_cores_materiais.py` gera `%TEMP%\materiais_cores.json` no PC (cor média de 12.971 texturas). **EM ESPERA** a pedido do João. O motor da nuvem já lê essa tabela quando existir.

## PENDENTE / PRÓXIMO

0. João vai atualizar XML + DXF da `COZINHA 2` (com pedra, eletros, janela) → trazer e regerar; cotas devem mostrar janela/pedra/eletros como referência (ver prancha 05 do caderno aprovado). João conferir Cozinha 2 e Escritório na v10. Pontos vistos: cotas da planta (prancha 03) amontoadas; Painel Freijó 719x18x364 não está no DXF.
1. Cores reais (em espera): integrar `materiais_cores.json`.
2. Levar a v10 para o PC (`motor v10`) quando o João aprovar.
3. Testar em um 3º projeto novo (cliente novo) para validar que o motor generaliza.
4. Depois: cadernos Nadecor (Produção peça a peça, Instalação).
