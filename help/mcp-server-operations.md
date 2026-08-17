---
title: Marketo Engage MCP operations
description: Learn which Marketo Engage MCP operations are available for use with AI assistants.
autotag-review: '2026-06-02T13:31:42.084Z'
TQID: 'https://experienceleague.adobe.com/qvrWbHOCsCCHctduNDxMhkE8JAKxZk8FCYfKvzxfcYA'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
---

# [!DNL Marketo Engage] MCP operations

The following operations are available through the [!DNL Marketo Engage] MCP server. The server provides read-only or non-destructive endpoints. The AI system cannot use `Delete` or other destructive operations.

>[!NOTE]
>
>The MCP Server team is working on enabling the Smart List and Smart Campaign Asset APIs to work with the MCP Server. This work, including allowlisting items, is expected to be finished in Q3 2026.

For information on how data is handled with Marketo AI and the Marketo Engage MCP server, see the [Data Information](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-ai/data-information) page.

## Bulk export

[Bulk export API reference](https://developer.adobe.com/marketo-apis/api/mapi){target="_blank"}

- `bulk_export_create`
- `bulk_export_enqueue`
- `bulk_export_file`
- `bulk_export_status`
- `get_import_status`

## Channels and tags

[Channels API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels){target="_blank"} | [Tags API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags){target="_blank"}

- `browse_channels`
- `browse_tag_types`
- `get_channel_by_name`
- `get_tag_type_by_name`

## Emails

[Emails API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails){target="_blank"}

- `approve_email`
- `browse_emails`
- `create_email`
- `get_email_by_id`
- `get_email_by_name`
- `get_email_content`
- `update_email_content`

## Folders

[Folders API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders){target="_blank"}

- `browse_folders`
- `create_folder`
- `delete_folder`
- `get_folder_by_id`
- `get_folder_by_name`
- `get_folder_content`
- `update_folder`

## Forms

[Forms API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms){target="_blank"}

- `add_field_set`
- `add_field_to_form`
- `add_field_visibility_rule`
- `add_rich_text_field`
- `approve_form`
- `browse_forms`
- `clone_form`
- `create_form`
- `delete_field_from_fieldset`
- `delete_form`
- `delete_form_field`
- `discard_form_draft`
- `get_form_by_id`
- `get_form_by_name`
- `get_form_field_metadata`
- `get_form_fields`
- `get_forms_used_by`
- `get_program_member_fields`
- `get_thank_you_page`
- `set_field_autofill`
- `update_field_positions`
- `update_form`
- `update_form_field`

## Leads

[Leads API reference](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads){target="_blank"}

- `add_leads_to_list`
- `describe_lead`
- `get_activity_types`
- `get_lead_activities`
- `get_leads_by_filter`
- `get_leads_by_smart_list`
- `get_paging_token`

## Programs

[Programs API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs){target="_blank"}

- `approve_program`
- `browse_email_batch_programs`
- `browse_nurture_programs`
- `browse_program_details`
- `browse_program_events`
- `browse_programs`
- `browse_scheduled_programs`
- `clone_program`
- `create_program`
- `delete_program_tag`
- `get_program_by_id`
- `get_program_by_name`
- `get_program_creation_options`
- `get_program_smart_list`
- `get_programs_by_tag`
- `unapprove_program`
- `update_program`
- `update_program_tag`

## Smart campaigns

[Smart campaigns API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns){target="_blank"}

- `activate_smart_campaign`
- `add_flow_step`
- `browse_smart_campaigns`
- `create_smart_campaign`
- `facet_smart_campaigns`
- `get_smart_campaign_auto_suggest`
- `get_smart_campaign_by_id`
- `get_smart_campaign_by_name`
- `get_smart_campaign_flow_step_by_name`
- `get_smart_campaign_flow_step_type_by_name`
- `get_smart_campaign_flow_step_types`
- `get_smart_campaign_flow_steps`
- `get_smart_campaign_rule_by_name`
- `get_smart_campaign_rules`
- `get_smart_campaign_scheduled_runs`
- `get_smart_campaign_used_by`
- `get_smart_list_by_campaign_id`
- `schedule_campaign`
- `trigger_campaign`
- `update_flow_step_choice`
- `update_smart_campaign`

## Smart lists

[Smart lists API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Lists){target="_blank"}

- `add_smart_list_rule`
- `browse_smart_lists`
- `clone_smart_list`
- `create_smart_list`
- `delete_all_smart_list_rules`
- `get_smart_list_auto_suggest`
- `get_smart_list_by_id`
- `get_smart_list_by_name`
- `get_smart_list_rule_by_name`
- `get_smart_list_rules`
- `get_smart_list_used_by`
- `remove_smart_list_rule_constraint`
- `reorder_smart_list_rules`
- `update_smart_list_filter_logic`
- `update_smart_list_rule`

## Snippets

[Snippets API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets){target="_blank"}

- `approve_snippet`
- `browse_snippets`
- `clone_snippet`
- `create_snippet`
- `delete_snippet`
- `discard_snippet_draft`
- `facet_snippets`
- `get_snippet_by_id`
- `get_snippet_content`
- `get_snippet_dynamic_content`
- `unapprove_snippet`
- `update_snippet`
- `update_snippet_content`
- `update_snippet_dynamic_content`

## Static lists

[Static lists API reference](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists){target="_blank"}

- `browse_lists`
- `create_list`
- `get_list_by_id`
- `get_list_by_name`
- `get_list_members`
- `remove_from_list`
- `update_list`

## Tokens

[Tokens API reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens){target="_blank"}

- `create_calendar_token`
- `create_token`
- `delete_token`
- `get_calendar_tokens`
- `get_tokens_by_folder`

## MCP flow steps tools enabled

| Flow Steps | Triggers | Filters (activity) | Filters (attribute) |
| --- | --- | --- | --- |
| <ul><li>Add to Field Set</li><li>Add to List</li><li>Add to Microsoft Campaign</li><li>Add to Nurture</li><li>Add to SFDC Campaign</li><li>Call Webhook</li><li>Change Data Value</li><li>Change Lead Partition</li><li>Change Nurture Cadence</li><li>Change Nurture Track</li><li>Change Owner</li><li>Change Owner in Microsoft</li><li>Change Program Data</li><li>Change Program Member Data</li><li>Change Revenue Stage</li><li>Change Score</li><li>Change Segment</li><li>Change Status in Progression</li><li>Change Status in SFDC Campaign</li><li>Convert Lead</li><li>Create Task</li><li>Create Task in Microsoft</li><li>Delete Lead</li><li>Delete Lead from Microsoft</li><li>Delete Lead from SFDC</li><li>Execute Campaign</li><li>Interesting Moment</li><li>Remove from Field Set</li><li>Remove from Flow</li><li>Remove from List</li><li>Remove from Microsoft Campaign</li><li>Remove from SFDC Campaign</li><li>Request Campaign</li><li>Send Alert</li><li>Send Email</li><li>Sync Lead to Microsoft</li><li>Sync Lead to SFDC</li><li>Wait</li></ul> | <ul><li>Activity is Logged</li><li>Activity is Updated</li><li>Added to List</li><li>Added to Microsoft Campaign</li><li>Added to Nurture</li><li>Added to Opportunity</li><li>Added to Opportunity (Account)</li><li>Added to Opportunity (Contact)</li><li>Added to SFDC Campaign</li><li>Asks questions during event</li><li>Attends event</li><li>Campaign is Requested</li><li>Clicks Link</li><li>Clicks Link in Email</li><li>Clicks Link in Sales Email</li><li>Clicks Link in SMS Message</li><li>Clicks on a Link</li><li>Data Value Changes</li><li>Downloads an asset</li><li>Email Bounces</li><li>Email Bounces Soft</li><li>Email is Delivered</li><li>Engages with a Conversational Flow</li><li>Engages with a Dialogue</li><li>Engages with an Agent in Conversational Flow</li><li>Engages with an Agent in Dialogue</li><li>Fills Out Form</li><li>Has Interesting Moment</li><li>Interacts with Document in Conversational Flow</li><li>Interacts with Document in Dialogue</li><li>Is Sent Sales Email</li><li>Lead is Converted</li><li>Lead is Created</li><li>Lead is Deleted from Microsoft</li><li>Lead is Deleted from SFDC</li><li>Lead is Pushed to Marketo</li><li>Lead is Synced to Microsoft</li><li>Lead is Synced to SFDC</li><li>Lead Partition Changes</li><li>Manual Stage Change</li><li>Nurture Cadence Changes</li><li>Nurture Track Changes</li><li>Opens Email</li><li>Opens Sales Email</li><li>Opportunity (Account) is Updated</li><li>Opportunity (Contact) is Updated</li><li>Opportunity is Updated</li><li>Owner Changes</li><li>Owner Changes in Microsoft</li><li>Program Member Data is Changed</li><li>Progression Status is Changed</li><li>Reaches Dialogue Goal</li><li>Reaches Goal in Conversational Flow</li><li>Received Forward to Friend Email</li><li>Removed from List</li><li>Removed from Microsoft Campaign</li><li>Removed from Opportunity</li><li>Removed from Opportunity (Account)</li><li>Removed from Opportunity (Contact)</li><li>Removed from SFDC Campaign</li><li>Replies to Sales Email</li><li>Responds to a Poll</li><li>Responds to a Survey</li><li>Revenue Stage is Changed</li><li>Sales Email Bounces</li><li>Sales Email is Received</li><li>Schedules Meeting in Conversational Flow</li><li>Schedules Meeting in Dialogue</li><li>Score is Changed</li><li>Segment Changes</li><li>Sent Alert</li><li>Sent Forward to Friend Email</li><li>SMS Message Bounces</li><li>SMS Message is Delivered</li><li>Status is Changed in SFDC Campaign</li><li>Unsubscribes from Email</li><li>Visits Web Page</li><li>Webhook is Called</li></ul> | <ul><li>Activity was Logged</li><li>Activity was Updated</li><li>Alert Was Sent</li><li>Campaign was Executed</li><li>Campaign was Requested</li><li>Click Link</li><li>Clicked Link in Email</li><li>Clicked Link in Sales Email</li><li>Clicked Link in SMS Message</li><li>Clicked on a Link</li><li>Data Value Changed</li><li>Downloaded an asset</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Engaged with a Conversational Flow</li><li>Engaged with a Dialogue</li><li>Engaged with an Agent in Conversational Flow</li><li>Engaged with an Agent in Dialogue</li><li>Filled Out Form</li><li>Had Interesting Moment</li><li>Has asked questions during event</li><li>Has attended event</li><li>Interacted with Document in Conversational Flow</li><li>Interacted with Document in Dialogue</li><li>Lead Partition Changed</li><li>Lead was Converted</li><li>Lead was Created</li><li>Lead was Deleted from Microsoft</li><li>Lead was Deleted from SFDC</li><li>Lead was Pushed to Marketo</li><li>Lead was Synced to Microsoft</li><li>Lead was Synced to SFDC</li><li>Nurture Cadence Changed</li><li>Nurture Track Changed</li><li>Opened Email</li><li>Opened Sales Email</li><li>Opportunity (Account) was Updated</li><li>Opportunity (Contact) was Updated</li><li>Opportunity was Updated</li><li>Owner was Changed</li><li>Owner was Changed in Microsoft</li><li>Program Member Data was Changed</li><li>Progression Status was Changed</li><li>Reached Dialogue Goal</li><li>Reached Goal in Conversational Flow</li><li>Received Forward to Friend Email</li><li>Replied to Sales Email</li><li>Responded to a Poll</li><li>Responded to a Survey</li><li>Revenue Stage was Changed</li><li>Sales Email Bounced</li><li>Sales Email was Received</li><li>Scheduled Meeting in Conversational Flow</li><li>Scheduled Meeting in Dialogue</li><li>Score was Changed</li><li>Segment Changed</li><li>Sent Forward to Friend Email</li><li>SMS Message Bounced</li><li>Unsubscribed from Email</li><li>Visited Web Page</li><li>Was Added to List</li><li>Was Added to Nurture</li><li>Was Added to Opportunity</li><li>Was Added to Opportunity (Account)</li><li>Was Added to Opportunity (Contact)</li><li>Was Delivered Email</li><li>Was Delivered SMS Message</li><li>Was Removed from List</li><li>Was Removed from Opportunity</li><li>Was Removed from Opportunity (Account)</li><li>Was Removed from Opportunity (Contact)</li><li>Was Sent Email</li><li>Was Sent Sales Email</li><li>Webhook is Called</li></ul> | <ul><li>Account Owner Email Address</li><li>Account Owner First Name</li><li>Account Owner Last Name</li><li>Acquisition Date</li><li>Acquisition Program</li><li>Acquisition Program Name</li><li>Address</li><li>Annual Revenue</li><li>Anonymous IP</li><li>Billing Address</li><li>Billing City</li><li>Billing Country</li><li>Billing Postal Code</li><li>Billing State</li><li>Black Listed</li><li>City</li><li>Company Microsoft Type</li><li>Company Name</li><li>Country</li><li>Created At</li><li>Date of Birth</li><li>Department</li><li>Do Not Call</li><li>Do Not Call Reason</li><li>Duplicate Fields</li><li>Email Address</li><li>Email Invalid</li><li>Email Invalid Cause</li><li>Email Suspended</li><li>Email Suspended At</li><li>Email Suspended Cause</li><li>Fax Number</li><li>First Name</li><li>Full Name</li><li>Has Opportunity</li><li>Industry</li><li>Inferred City</li><li>Inferred Company</li><li>Inferred Country</li><li>Inferred Metropolitan Area</li><li>Inferred Phone Area Code</li><li>Inferred Postal Code</li><li>Inferred State Region</li><li>Is Customer</li><li>Is Partner</li><li>Job Title</li><li>Last Name</li><li>Lead Owner Email Address</li><li>Lead Owner First Name</li><li>Lead Owner Job Title</li><li>Lead Owner Last Name</li><li>Lead Owner Phone Number</li><li>Lead Partition Name</li><li>Lead Rating</li><li>Lead Score</li><li>Lead Source</li><li>Lead Status</li><li>Main Phone</li><li>Marketing Suspended</li><li>Member of Field Set</li><li>Member of List</li><li>Member of Nurture</li><li>Member of Program</li><li>Member of Revenue Model</li><li>Member of Revenue Stage</li><li>Member of SFDC Campaign</li><li>Member of Smart Campaign</li><li>Member of Smart List</li><li>Microsoft Account Num</li><li>Microsoft Created Date</li><li>Microsoft Is Deleted</li><li>Microsoft Type</li><li>Middle Name</li><li>Mobile Phone Number</li><li>Notes</li><li>Num Employees</li><li>Number of Opportunities</li><li>Original Referrer</li><li>Original Search Engine</li><li>Original Search Phrase</li><li>Original Source Info</li><li>Original Source Type</li><li>Parent Company Name</li><li>Person Time Zone</li><li>Phone Number</li><li>Postal Code</li><li>Random Sample</li><li>Registration Source Info</li><li>Registration Source Type</li><li>Role</li><li>Salutation</li><li>SFDC Account Num</li><li>SFDC Created Date</li><li>SFDC Is Deleted</li><li>SFDC Type</li><li>SIC Code</li><li>Site</li><li>State</li><li>Total Opportunity Amount</li><li>Total Opportunity Expected Revenue</li><li>Unsubscribed</li><li>Unsubscribed Reason</li><li>Updated At</li><li>Website</li></ul> |

{style="table-layout:auto"}
