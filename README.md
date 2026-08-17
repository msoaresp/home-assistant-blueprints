# Home Assistant Blueprints

Repositório de blueprints personalizados para Home Assistant.

## Estrutura

```text
home-assistant-blueprints/
├── automation/
│   ├── threeway_virtual.yaml
│   └── wasp_j2_13_ocupacao_super_otimizada.yaml
├── script/
└── template/
```

As pastas `script/` e `template/` ficam reservadas para futuros blueprints desses tipos.

## Blueprints disponíveis

### ThreeWay Virtual

Sincroniza múltiplas entidades `light` e `switch`, criando um comportamento semelhante a interruptores paralelos virtuais.

Principais recursos:

- sincronização bidirecional entre os pontos selecionados;
- proteção contra loops e realimentações;
- ignora entidades em estado `unavailable` ou `unknown`;
- reconciliação após reinício do Home Assistant;
- reconciliação quando uma entidade volta a ficar disponível;
- maioria dos estados válidos define o estado do grupo;
- em caso de empate, prevalece `off` por segurança.

Arquivo:

`automation/threeway_virtual.yaml`

URL de importação:

`https://github.com/msoaresp/home-assistant-blueprints/blob/main/automation/threeway_virtual.yaml`

### WASP J2-13 - Ocupação Super Otimizada

Gerencia ocupação de ambientes utilizando sensor de porta, sensor de movimento, helpers e timer.

Recursos principais:

- marca o ambiente como ocupado ao detectar movimento;
- cancela o timer de desocupação quando há novo movimento;
- inicia ou reinicia o timer quando a porta muda de estado;
- confirma ausência antes de desocupar;
- desocupa diretamente após 1 hora contínua sem movimento;
- controla luz principal e luzes adicionais opcionais;
- não usa o helper de ocupação como gatilho, evitando autoacionamento da própria automação.

Helpers utilizados:

- `input_boolean` de ocupação: registra se o ambiente está ocupado;
- `input_boolean` de habilitação: ativa ou desativa a automação;
- `timer`: controla a confirmação de desocupação.

Arquivo:

`automation/wasp_j2_13_ocupacao_super_otimizada.yaml`

URL de importação:

`https://github.com/msoaresp/home-assistant-blueprints/blob/main/automation/wasp_j2_13_ocupacao_super_otimizada.yaml`

## Importação pelo Home Assistant

No Home Assistant, acesse:

**Configurações → Automações e Cenas → Blueprints → Importar Blueprint**

Cole a URL do blueprint desejado.

## Instalação manual

Os blueprints de automação também podem ser copiados diretamente para:

`/config/blueprints/automation/`

Exemplo:

```text
/config/blueprints/automation/
├── threeway_virtual.yaml
└── wasp_j2_13_ocupacao_super_otimizada.yaml
```

Depois de alterar ou adicionar arquivos manualmente, recarregue as automações ou reinicie o Home Assistant.

## Organização futura

O repositório deve manter cada tipo de blueprint em sua própria pasta:

```text
automation/
script/
template/
```

## Manutenção

Sempre que um blueprint for alterado, mantenha também atualizado o campo `source_url` dentro do próprio YAML para permitir futuras reimportações pelo Home Assistant.
