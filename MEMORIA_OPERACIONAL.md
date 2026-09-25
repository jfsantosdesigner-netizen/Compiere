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

1. Sequência: Capa → Contrato → Planta+Especificações → Visão Geral → por vista: Listagem, Cotas. Pranchas = 4 + 2 × nº de vistas.
2. LISTAGEM: 3D FRONTAL (câmera na FRENTE dos móveis, nunca nas costas), PORTAS FECHADAS, com paredes, balões amarelos. Tabela Item | Descrição | Dimensão. Lista só módulos, tamponamentos e fechamentos. Sem cotas.
3. COTAS: 2D FRONTAL, PORTAS ABERTAS, com paredes (só como referência). Cotar só módulos inteiros + alturas de prateleiras. Nada externo (janela, piso, eletro).
4. ESPECIFICAÇÕES (prancha 03): cores (caixa, portas, tamponamentos) + FERRAGENS (dobradiças, corrediças, puxadores, portas de alumínio/vidros/espelhos) + espessuras. Ferragens só nessa prancha.
5. Imagens limpas: peças desenhadas como caixas, só bordas, sem riscos de triangulação.
6. Escala mínima 1:25. A4 paisagem, nada encosta no quadro.
7. Fonte de dados: XML MONTADO + DXF exportados do Promob. Explodido = só Produção Nadecor. SketchUp/3DS não são usados.

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

## PENDENTE / PRÓXIMO

0. **BUG**: a prancha 02 (Contrato) mostra o cabeçalho antigo da Cozinha (`assets\CONTRATO.pdf` é a página inteira do caderno aprovado). Recortar só o texto do contrato.
1. João conferir o Escritório regerado na v8 (verificar se dobradiça/cabideiro ainda aparecem sobre as portas no 3D e se as cores reais e a capa nova estão certas).
2. Regerar a Cozinha com as regras atuais e conferir.
3. Testar em um 3º projeto novo (cliente novo) para validar que o motor generaliza.
4. Depois: cadernos Nadecor (Produção peça a peça, Instalação).
