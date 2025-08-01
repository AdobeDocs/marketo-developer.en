## Getting Started

Marketo Engage is a marketing automation platform that enables marketers to manage personalized multi-channel programs and campaigns to prospects and customers. The Marketo Engage platform can be extended using integration points. Below you find the core entities and their relationships.

>[!NOTE]
>The SOAP API is being deprecated and will no longer be available after October 31st 2025. All new development should be done with the Marketo [REST API](./rest-api/rest-api.md), and existing services should be migrated by that date to avoid interruptions in service. If you have a service which uses the SOAP API, please consult the SOAP API [Migration Guide](./soap-api/migration.md) for information on how to migrate.
>

When either the Native SFDC or MS Dynamics CRM connection is enabled on a Marketo Engage instance, the following objects are Read-Only: Company, Opportunity, Opportunity Role, Sales Person

![Data Model](assets/data_model.png)

## Person (Leads)

People are the founddation of any marketing automation platform. Within Marketo, all non-sales person records are referred to as leads, regardless of whether they are designated as leads, prospects, suspects, contacts, and so forth, from a sales perspective. The lead object comes with a set of standard fields, such as email, first name and last name. Additional fields can be added to the lead object type to extend the types of information assocdiated with records in the system. Custom attributes can be read and written to just as the standard fields. A complete list of fields can be found within the Marketo **[!UICONTROL Admin]** > **[!UICONTROL Field Management]** menu. Leads are uniquely identified in Marketo by the id field. Other unique keys must be enforced externally from the system.
