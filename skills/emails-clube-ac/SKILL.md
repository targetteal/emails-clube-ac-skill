---
name: emails-clube-ac
description: Criar ou revisar e-mails HTML do Clube dos Agentes de Mudança para campanhas e automações no ActiveCampaign, com a identidade do Clube e arquivo pronto para colar no editor. Use para qualquer tema de e-mail do Clube, não apenas a abertura.
---

# E-mails do Clube no ActiveCampaign

Produza uma peça com assunto sugerido, pré-cabeçalho e HTML independente. Entregue um arquivo `.html` que a pessoa possa abrir e copiar para o ActiveCampaign; se ela pedir o código na conversa, inclua-o também. Elaborar o arquivo não autoriza criar campanhas, alterar automações, programar envios ou disparar mensagens.

## Antes de escrever

- Identifique propósito, público, momento de envio e ação principal. Confirme datas, fuso, preço, promessas, link de destino e imagem em fontes do projeto ou com o usuário; não invente esses dados.
- Se o pedido ainda estiver aberto, proponha um rascunho editorial antes de fixar detalhes incertos. Prefira português caloroso, direto e falado, sem marketing genérico nem urgência artificial.
- Leia apenas os exemplos pertinentes em `references/`. Eles mostram a gramática visual e a diferença entre boas-vindas, lembrete e e-mail no horário do evento; seus textos, horários e links não são padrões para outros temas.
- Quando houver repositório do Clube disponível, confira `docs/brand/design.md` e os assets atuais antes de decidir se mantém a composição dos exemplos. Uma campanha nova pode pedir outra imagem, outra ênfase ou até um e-mail sem capa.

## Composição

- Mantenha reconhecimento do Clube: nome por extenso no topo, paleta editorial com azul-petróleo `#256675`, fundo claro `#f9f7f4` e azul-pálido `#dcebed` quando fizer sentido. Use hierarquia tipográfica forte, texto respirado e uma ação principal coerente com o momento.
- Os exemplos usam tabelas de apresentação, CSS inline e largura máxima de 600 px para funcionar em clientes de e-mail. Inclua pré-cabeçalho oculto, `alt` útil para imagens, URL absoluta HTTPS para assets e um link legível como alternativa ao botão principal.
- Não copie automaticamente a capa da Temporada 0 ou a marcação “Temporada 0” para outro assunto. Se usar imagem, verifique que a URL pública responde e que ela continua legível em tela pequena.
- Antes de um evento, uma ação de calendário pode ser mais útil que um botão para entrar na sala. No horário do evento, o link de acesso pode ser a ação principal. Escolha pela utilidade naquele envio, não por fórmula fixa.
- Para um HTML independente do ActiveCampaign, use o rodapé de descadastro apropriado, por exemplo `%UNSUBSCRIBELINK%` quando a campanha for enviada a uma lista. Confirme no preview do AC se o editor já adiciona rodapé e se as tags de personalização foram substituídas. Se houver dúvida sobre uma tag, confira a documentação atual do ActiveCampaign.

## Entrega e verificação

- Revise o texto e os links com o contexto específico do envio. Verifique datas e fusos, CTA, assunto, pré-cabeçalho, URL de imagem, descadastro e ausência de conteúdo obsoleto dos exemplos.
- Abra o HTML em viewport estreito e largo; confira imagem, leitura, botão e ausência de rolagem horizontal. Um preview local não prova a renderização no ActiveCampaign: peça um envio de teste pelo AC antes de programar a campanha.
- Diga claramente se entregou só o arquivo ou se uma automação/envio foi de fato configurado.

## Operação no ActiveCampaign (rascunhos via API v3)

Criar rascunho de campanha por código, sem encostar no que já foi enviado:

1. Casca: `POST /api/3/campaign` com `{"type": "single", "name": "...", "canSplitContent": false}` → retorna `id`. (O endpoint plural `/campaigns` exige `listIds` + `messages` inline e devolve 422 — não usar para criar.)
2. Mensagem: `POST /api/3/messages` com `subject`, `fromname`, `fromemail`, `reply2`, `html`, `text` → retorna `message.id`.
3. Vínculo: `POST /api/3/campaignMessages` com `{"campaignMessage": {"campaignid": ..., "messageid": ...}}`.
4. Conferência: `GET /api/3/campaigns/{id}` deve mostrar `status: "0"` (rascunho) e `GET campaigns/{id}/campaignMessage` o assunto linkado.

Limites reais da API (validados em 2026-09):

- Associar lista é só pelo painel — `campaignLists` aceita apenas GET. Escolha a lista na UI antes de qualquer teste de envio.
- `PUT /api/3/messages/{id}` atualiza HTML/texto de rascunho sem criar peça nova; o original nunca é alterado ao copiar (ler o HTML dele e gravar na mensagem do rascunho).
- Marque rascunhos de teste com `[TESTE]` no nome/assunto para ninguém confundir no painel.
- Nunca programe nem dispare envio sem pedido explícito do usuário; rascunho ≠ autorização.

## Referências deste processo

- [Boas-vindas da lista de abertura](references/boas-vindas-activecampaign.html): confirmação imediata, convite ao calendário e link da sala discreto.
- [Lembrete do dia do encontro](references/lembrete-encontro-abertura-activecampaign.html): contexto do encontro e link da sala em destaque.
- [E-mail das 20h](references/encontro-comecou-activecampaign.html): mensagem curta para o início do encontro, com acesso imediato.

Os arquivos em `references/` são cópias de exemplos concluídos. Use-os como referência visual e editorial; atualize fatos, links, audiência e oferta em cada novo e-mail.
