---
title: "Forms API Reference"
description: "Forms API Reference"
feature: "Forms"
---

# Forms API Reference

There are two main objects that you will interact with using the Forms 2.0 API. The MktoForms2 object and the Form object. The MktoForms2 object is the top-level publicly visible namespace for Forms2 functionality and contains functions to create, load, and fetch Form objects.

## MktoForms2 Methods

<table><tbody><tr valign="top"><td><strong>Method</strong></td><td><strong>Description</strong></td><td><strong>Parameters</strong></td><td><strong>Returns</strong></td></tr><tr valign="top"><td>.loadForm(baseUrl, munchkinId, formId, callback)</td><td>Loads a form descriptor from Marketo servers and creates a new Form object.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>baseUrl</td><td>String</td><td>URL to the Marketo server instance for your subscription</td></tr><tr><td>munchkinId</td><td>String</td><td>Munchkin ID of the subscription</td></tr><tr><td>formId</td><td>String or Number</td><td>The form version id (Vid) of the form to load</td></tr><tr><td>callback (optional)</td><td>Function</td><td>A callback function to pass the constructed Form object to once it has been loaded and initialized.</td></tr></tbody></table></td><td>undefined</td></tr><tr valign="top"><td>.lightbox(form, opts)</td><td>Renders a lightbox style modal dialog with the Form object in it.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>form</td><td>Form Object</td><td>An instance of a Form object that you want to have rendered in a lightbox.</td></tr><tr><td>opts (optional)</td><td>Object</td><td>An object of options passed to the lightbox object</td></tr><tr><td><ul><li>onSuccess</li></ul></td><td>Function</td><td>A callback that will be triggered when the form is submitted.</td></tr><tr><td><ul><li>closeBtn</li></ul></td><td>Boolean default true</td><td>Controls if a close button (X) is displayed on the lightbox dialog.</td></tr></tbody></table></td><td>A lightbox object with .show() and .hide() methods.</td></tr><tr valign="top"><td>.newForm(formData, callback)</td><td>Creates a new Form object from a Form Descriptor JS object.<div></div>Adds a callback function that will be called once all stylesheets and known lead information has been fetched and the Form object has been created.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>formData</td><td>Form Descriptor Object</td><td>A form descriptor object, as created by the Marketo Forms V2 Editor</td></tr><tr><td>callback (optional)</td><td>Function</td><td>This callback will be called with a single argument, a newly created instance of Form object.</td></tr></tbody></table></td><td>undefined</td></tr><tr valign="top"><td>.getForm(formId)</td><td>Gets a previously created Form object by form identifier</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>formId</td><td>Number or String</td><td>Form Vid Identifier.</td></tr></tbody></table></td><td>Form Object</td></tr><tr valign="top"><td>.allForms()</td><td>Fetches an array of all form objects that have been previously constructed on the page.</td><td>n/a</td><td>Array of Form Object</td></tr><tr valign="top"><td>.getPageFields()</td><td>Gets a JS object containing data from the url and referrer that may be interesting for tracking purposes.</td><td>n/a</td><td>Object</td></tr><tr valign="top"><td>.whenReady(callback)</td><td>Adds a callback that will be called exactly once for each form on the page that becomes "ready". Readiness means that the form exists, has been initially rendered and had its initial callbacks called.<p class="p1">If there is already a form that is ready at the time this function is called, the passed callback will be called immediately.</p></td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td><p class="p1">The callback is passed a single argument, a form object.</p></td></tr></tbody></table></td><td>MktoForms2 Object</td></tr><tr valign="top"><td>.onFormRender(callback)</td><td>Adds a callback that will be called every time any form on the page renders. Forms are rendered when initially created, then again every time that visibility rules alter the structure of the form.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td>The callback will be passed a single argument, the form object of the form that was rendered.</td></tr></tbody></table></td><td>MktoForms2 Object</td></tr><tr valign="top"><td>.whenRendered(callback)</td><td>Like onFormRender, this adds a callback that will be called every time a form is rendered. Additionally, this will also call the callback immediately for all forms that have already been rendered.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td>The callback will be passed a single argument, the form object of the rendered form.</td></tr></tbody></table></td><td>MktoForms2 Object</td></tr></tbody></table>

## Form Methods

<table><tbody><tr valign="top"><td><strong>Method</strong></td><td><strong>Description</strong></td><td><strong>Parameters</strong></td><td><strong>Returns</strong></td></tr><tr valign="top"><td>.render(formElem)</td><td>Renders a form object, returning a jQuery object wrapping a form element that contains the form. If passed a formElem, it will use that as the form element, otherwise it will create a new one.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>formElem (optional)</td><td>jQuery Object</td><td>A jQuery wrapped form element into which to render.</td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>jQuery Object</td><td>A jQuery wrapped form element containing the rendered form.</td></tr></tbody></table></td></tr><tr valign="top"><td>.getId()</td><td>Gets the id of the form.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Number</td><td>The id of the form object that this form represents</td></tr></tbody></table></td></tr><tr valign="top"><td>.getFormElem()</td><td>Gets the jQuery wrapped form element of a rendered form.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>jQuery Object</td><td>A jQuery wrapped form element or null if the form has not been rendered with the render() method yet.</td></tr></tbody></table></td></tr><tr valign="top"><td>.validate()</td><td>Forces the form to validate, highlighting any errors that may exist and returning the result. Does not submit the form.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Boolean</td><td>Returns true if all the validators on the form passed, false otherwise.</td></tr></tbody></table></td></tr><tr valign="top"><td>.onValidate(callback)</td><td>Adds a validation callback that will be called anytime validation is triggered.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td>A callback that will be triggered any time that validation occurs. The callback will be passed one parameter, a boolean stating if the validation had succeeded.</td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Form Object</td><td>The same form object on which the method was called, for chaining purposes.</td></tr></tbody></table></td></tr><tr valign="top"><td>.submit()</td><td>Triggers the form's submit event. This will start the from submit flow, performing validation, firing any onSubmit events, submitting the form, and firing any onSuccess events if form submission was successful.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Form Object</td><td>The same form object on which the method was called, for chaining purposes.</td></tr></tbody></table></td></tr><tr valign="top"><td>.onSubmit(callback)</td><td>Adds a callback that will be called when the form is submitted. This is fired when the submission begins, before the success/failure of the request is known.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td>A function that will be called when the form is submitted. This callback will be passed one argument, this Form object.</td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Form Object</td><td>The same form object on which the method was called, for chaining purposes.</td></tr></tbody></table></td></tr><tr valign="top"><td>.onSuccess(callback)</td><td>Adds a callback that will be called when the form has been successfully submitted but before the lead is forwarded to the follow up page. Can be used to prevent the lead from being forwarded to the follow up page after successful submission.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>callback</td><td>Function</td><td>A function that will be called when the form has been successfully submitted. This callback will be passed two arguments. A JS Object containing the values that were submitted and a String url of the follow up page that the user will be forwarded to, or null or empty string if there is no configured follow up page.<div></div>Special behavior: If this callback returns a <em style="font-family: inherit;">false </em><span style="font-family: inherit;">(measured using ===) then the visitor will NOT be forwarded to the follow up page and the page will NOT be reloaded. This allows the implementor to do extra processing to the follow up url, or to take action on page using JavaScript instead of leaving the page.</span></td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Form Object</td><td>The same form object on which the method was called, for chaining purposes.</td></tr></tbody></table></td></tr><tr valign="top"><td>.submittable(canSubmit) <em>also available as:</em> <em>.submitable(canSubmit)</em></td><td>Gets or sets whether the form can be submitted. If called with no arguments, it gets the value, if called with one argument it sets the value.This can be used to prevent a form from being submitted while other criteria outside of the normal form must be fulfilled.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>canSubmit (optional)</td><td>Boolean</td><td>Sets the form to be submittable or non submittable.</td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Boolean or Form Object</td><td>If called with no arguments, returns a boolean indicating if the form is submittable. If called with one argument, returns this Form Object for chaining purposes.</td></tr></tbody></table></td></tr><tr valign="top"><td>.allFieldsFilled()</td><td>Returns true if all the fields in the form have non-blank values set.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Boolean</td><td>True if all fields have non-blank/empty/unset/null values, false otherwise.</td></tr></tbody></table></td></tr><tr valign="top"><td>.setValues(vals)</td><td>Sets values on one or more fields in the form.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>vals</td><td>Object</td><td>A JS Object. For each key/value pair in the object, the form field named key will be set to value.</td></tr></tbody></table></td><td>undefined</td></tr><tr valign="top"><td>.getValues()</td><td>Gets all the values of all the fields in the form.</td><td>n/a</td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Object</td><td>A JS Object containing key/value pairs representing the names and values of the fields in the form.</td></tr></tbody></table></td></tr><tr valign="top"><td>.addHiddenFields(values)</td><td>Adds input type=hidden fields to the form.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>values</td><td>Object</td><td>A JS Object containing key/value pairs representing the names and values of the hidden fields to add to the form.</td></tr></tbody></table></td><td>undefined</td></tr><tr valign="top"><td>.vals(values)</td><td>jQuery style .vals() setter/getter. If called with no arguments, is equivalent to calling getValues(). If called with one argument, is equivalent to calling setValues()</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>values (optional)</td><td>Object</td><td></td></tr></tbody></table><strong><strong><strong></strong></strong></strong></td><td>undefined</td></tr><tr valign="top"><td>.showErrorMessage(msg, elem)</td><td>Shows an error message, pointing at elem.</td><td><table><tbody><tr><td><strong>Name</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>msg</td><td>String of HTML</td><td>A string containing the text of the error you want to show.</td></tr><tr><td>elem (optional)</td><td>jQuery Object</td><td>The element for the error to point to. If unset, the form's submit button is used.</td></tr></tbody></table></td><td><table><tbody><tr><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td>Form Object</td><td>This Form object, for chaining.</td></tr></tbody></table></td></tr></tbody></table>