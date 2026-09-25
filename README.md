# E-mails do Clube no ActiveCampaign

Skill para criar e revisar e-mails HTML do Clube dos Agentes de Mudança. O repositório inclui o guia editorial, metadados do Codex e três exemplos completos. A skill não cria campanhas nem envia mensagens.

## Instalar no Hermes

```sh
hermes skills install targetteal/emails-clube-ac-skill/skills/emails-clube-ac
```

Isso instala a skill no perfil Hermes ativo. No perfil `default`, ela fica em `~/.hermes/skills/emails-clube-ac`.

## Instalar com o CLI skills em outros agentes

```sh
npx skills add targetteal/emails-clube-ac-skill --skill emails-clube-ac --agent '*' --global --yes
```

Para instalar só no Hermes pelo CLI:

```sh
npx skills add targetteal/emails-clube-ac-skill --skill emails-clube-ac --agent hermes-agent --global --yes
```

## Conteúdo

- `skills/emails-clube-ac/SKILL.md`: instruções editoriais e de produção.
- `skills/emails-clube-ac/references/`: três exemplos HTML completos.
- `skills/emails-clube-ac/agents/openai.yaml`: metadados de interface do Codex.

Distribuído sob a licença MIT. Instalar a skill não autoriza configurar campanhas, automações ou envios no ActiveCampaign.
