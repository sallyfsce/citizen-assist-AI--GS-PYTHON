# Citizen Assist AI

Assistente de terminal em Python que orienta **jovens no primeiro emprego** sobre documentos e direitos básicos (carteira de trabalho digital, CPF, título de eleitor, FGTS etc.), usando apenas uma base de conhecimento em JSON, com fonte e data de verificação em toda resposta.

## Integrantes
| Nome | RM |
|------|----|
| Aneliza | 572977 |
| Rafaella Ferreira | 571030 |


## Público e problema
- **Público:** jovens que estão procurando o primeiro emprego.
- **Problema:** a informação sobre documentos e direitos existe, mas está espalhada, em linguagem técnica e misturada com páginas que parecem oficiais e não são.

## ODS relacionados
- ODS 8 – Trabalho decente e crescimento econômico
- ODS 16 – Paz, justiça e instituições eficazes (acesso à informação)

## Como executar
Requisitos: Python 3 (não usa bibliotecas externas).

```
python main.py
```

Menu: 1) perguntar em texto livre, 2) navegar por categorias, 3) ver indicadores, 4) exportar CSV, 0) sair (pede nota de facilidade de 1 a 5).

## Estrutura
```
citizen-assist-ai/
├── README.md
├── main.py              # menu principal
├── orientacao.py        # classe Orientacao
├── base_conhecimento.py # classe BaseConhecimento + normalizar()
├── assistente.py        # classe Assistente
└── data/
    ├── base_conhecimento.json
    ├── historico.json
    └── atendimentos.csv
```

## Regra de pontuação
A pergunta e as palavras-chave/títulos passam por `normalizar()` (minúsculas, sem acentos, sem pontuação).
- +3 pontos por palavra-chave da orientação que aparece na pergunta
- +1 ponto por palavra da pergunta (4 letras ou mais) que aparece no título
- 6 pontos ou mais: confiança **ALTA** | 3 a 5 pontos: confiança **MÉDIA** | menos de 3: "Não encontrei" (sugere outras palavras e as categorias)
- `buscar()` devolve lista de tuplas `(pontos, orientacao)` da maior para a menor; o assistente mostra a melhor e até duas alternativas com 3 pontos ou mais.

## Regras de atendimento
- Nunca pede nome, CPF, telefone ou e-mail. Pergunta com 8 ou mais dígitos ou com `@` é recusada e **não é registrada**.
- Entradas inválidas (letras, fora da faixa, vazio, s/n inválido) não encerram o programa.
- JSON ausente ou corrompido não trava o programa.
- Toda resposta mostra fonte, data de verificação e o aviso de que o assistente não é canal oficial.

## Histórico, indicadores e CSV
Cada atendimento vai para `data/historico.json` (data, origem, pergunta, id da orientação, encontrou, ajudou, tentativas, tempo em segundos, nota). Indicadores: resposta encontrada (%), taxa de acerto (%), tempo médio para encontrar, tentativas por atendimento, facilidade de uso (1 a 5) e lista de dúvidas sem solução. Exportação para `data/atendimentos.csv` com `csv.DictWriter`.

## Integrações com outras disciplinas
(preencher se houver; caso contrário, escrever "Nenhuma")

## Fontes consultadas
- https://www.gov.br/pt-br/servicos/obter-a-carteira-de-trabalho
- https://www.gov.br/trabalho-e-emprego
- https://www.gov.br/receitafederal
- https://www.tse.jus.br
- https://www.caixa.gov.br
- https://meu.inss.gov.br
- https://www.gov.br

(Conferir cada página e atualizar o campo `verificado_em` no JSON.)

## Resultado do teste com usuários
- Pessoas de fora da equipe: (mínimo 3) | Atendimentos: (mínimo 10)
- Resposta encontrada: __% | Taxa de acerto: __% | Tempo médio: __ s | Tentativas: __ | Facilidade: __/5
- Dúvidas sem solução: (listar)
- Melhoria feita a partir do teste: (ex.: nova palavra-chave X na orientação Y)

(Não registrar nomes nem dados das pessoas.)

## Limitações
- A busca é por regras: não entende sinônimos que não estão nas palavras-chave nem erros de digitação.
- A base tem poucas orientações e é nacional; procedimentos locais podem variar.
- O conteúdo precisa ser reconferido nas fontes oficiais de tempos em tempos.

## Vídeo técnico
Link (YouTube, não listado): (preencher)
