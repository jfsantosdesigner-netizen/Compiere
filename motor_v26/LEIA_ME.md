# Motor v26 — cópia de segurança (o repositório do motor recusou o envio nesta sessão)

Base: motor v25 (ramo `v25` / `main` do `motor-cadernos-compiere`).
Arquivos alterados da v25 para a v26: `gerar_caderno.py`, `geo.py`, `VERSAO.txt`, `padrao.json`,
`ferramentas/visualizador.py`, `config_cozinha_v2.json`, `config_escritorio.json`.
O diff linha a linha está em `MUDANCAS_v25_para_v26.diff`.

Para montar a v26: pegar a v25 e substituir esses arquivos pelos desta pasta.
Projeto novo de teste: `exemplos/PRISCILA_COZINHA` (XML + DXF + config).

## Regras novas (condições: só atuam quando o projeto tem a situação)
1. PAREDE CORTADA POR PILAR / VÃO -> duas vistas (lado da cozinha / lado da churrasqueira).
2. CONJUNTO DE PAINÉIS SEM MÓDULO -> bloco próprio "PAINEL COM NICHOS" (3D frente + lateral, cotas).
3. PAINEL USINADO -> painel na frente de nichos abertos é desenhado com os vãos.
4. DIVISOR DE TALHER -> divisor de gaveta aceita peças até 750 mm.
5. MÓDULO BAIXO / GIRADO -> adega 150x870x600 é achada.
6. Porta avulsa do XML (ID POR_) não entra na listagem.
7. Peça duplicada do DXF (fora do XML) não é desenhada.
8. Detalhe de nicho não leva painel alto até o teto.
Barrote / cunha: NÃO entra (João).
