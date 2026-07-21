---
title: Webhooks
feature: Webhooks
description: Learn how to configure Marketo webhooks to call third-party services, set payload templates, encoding, response mappings, tokens, custom headers, and tips.
exl-id: fd283c66-05a1-4aa4-8412-0d41b8d1e3c8
TQID: https://experienceleague.adobe.com/r-GpAqhYPKvlDtMw5l23jeJWzlSqycP65eYJPA3m9EM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
    internal-label: Integrations
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
    internal-label: Administration
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
    internal-label: Templates
subfeature_v2:
  - id: ad89fb33-8541-4339-afe7-bb13d1633714
    internal-label: Flow Step
  - id: fc9b09fe-b844-4544-887b-e420c3b82065
    internal-label: Webhooks
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Webhooks

Marketo webhooks communicate with third-party web services. A webhook uses the GET or POST HTTP verb to send data to or retrieve data from a specific URL.

For instructions on creating a webhook and adding it to a Smart Campaign, see:

- [Create a Webhook](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [Call Webhook](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [Use a Webhook in a Smart Campaign](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

Configure each webhook with these properties:

- **[!UICONTROL URL]** - The URL to which you submit the web service request.
- **[!UICONTROL Request Type]** - The HTTP method.
- **[!UICONTROL Payload Template]** - The template for information sent in the POST body. Use any data format that supports HTTP POST, including XML, JSON, or SOAP. The serialization format must allow double quotes around strings. To insert a token, select **[!UICONTROL Insert Token]**. Marketo automatically encloses string-type tokens in double quotes.
- **[!UICONTROL Request Token Encoding]** - The request format, JSON or Form/Url, used to encode token values that include special characters such as an ampersand, '&'. Select the correct body encoding so that the webhook communicates with the web service correctly.
- **[!UICONTROL Response Type]** - The response format, JSON or XML. Select the correct type to map response properties to lead fields in Marketo.
- **[!UICONTROL Custom Headers]** - Key-Value pairs added as HTTP Headers through **[!UICONTROL Webhooks Actions]** > **[!UICONTROL Set Custom Header]**. You can add any number of custom headers.

Use [Response Mappings](response-mappings.md) to write data from web service responses back to leads.

## Tokens

All outgoing webhook fields, including URL, Template, and Custom Headers, populate token content in the same context as the flow step.

Lead and System tokens are always available. Trigger, Campaign, and Program tokens are available in their respective scopes. For more information, see:

- [Tokens Overview](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [System Tokens Glossary](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [Tokens for Interesting Moments](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

For example, when a Program or Campaign maps to a third-party resource, set an ID at the Program level as a `My Token`. Then pass the ID into the webhook request as a token.

## Custom Headers

Webhooks can send any number of Custom Header fields with an outgoing request. Add headers through **[!UICONTROL Webhooks Actions]** > **[!UICONTROL Set Custom Header]**.

Each header is a Key-Value pair and can contain tokens.

![Custom Headers](assets/custom-headers.png)

## Tips

- Use the Call Webhook flow step only in Trigger campaigns.
- Response mappings update a record only when the web service returns a 2xx HTTP response code.
- You can use web services to perform custom data enrichment, validation, or normalization from internal or external services.
- Webhook execution time depends on the response time of the service and can cause long campaign execution delays. Even if a service takes only 50ms to execute, 100,000 executions take 1.5 hours.
- Marketo waits up to 30 seconds for a given service call before terminating the call (also known as timing out).
- Marketo passes characters in the URL field as written. For example, '&' is sent as '&', and '%26' is sent as '%26'.
  - To send a percent-encoded character to the recipient server, explicitly pass the string that represents that character.
