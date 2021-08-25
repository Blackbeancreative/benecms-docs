# Developing with Bene

## Using RESTFUL API

### URL Formatting

All REST endpoints must require `projectId` as this is the unique identifier to pull the correct documents.

Your `projectId` can be found in the Pinco Console as a "Unique Name".

**Example URL**

`https://api.blackbeanpartners.com/rest/{projectId}/{collection}/{document}`

**If a collection and document are not provided in the URL:**

- A list of collections will be returned

**If a collection is provided and not a document in the URL:**

- A list of documents that belong to that collection will be returned

**If a collection and document are provided in the URL:**

- A list of data for that specific document will be returned

#### Finding Tagged Content

As of **July 29th, 2021**, the possibility of tagging different pieces of content has been added. However there is a key difference in finding tagged content through REST.

1. The URL is technically the same as the other endpoints however you **cannot** select a document directly, tagged content will only return a list of documents that are tagged under it. In order to select a document, you must use the `collectionId` provided in the item that's returned in the array.

**Example URL**

`https://api.blackbeanpartners.com/rest/{projectId}/tagged/{name}`

### Preview / Draft Mode

All documents can be set to a "Draft" mode which will hide the document from being provided in any endpoint unless `?preview=true` is included in the endpoint.

This can be a useful feature especially if using a Preview mode built into your framework such as Next JS.

### Development / Localhost

By default, our CMS enforces CORS however we have a few open URL's where development and testing will allow such requests.

- [http://localhost:3000](http://localhost:3000)
- [http://localhost:3001](http://localhost:3001)
- [http://localhost:8080](http://localhost:8080)

## Using Forms API

### Creating forms

Creating a valid form that can be processed by the CMS is fairly simple and only requires a few guidelines.

1. Your projectId must be a field inside of your form
2. Your form must contain a field labelled as `formName`
3. Your action (or if using ajax/fetch, endpoint) must be pointed towards: `https://api.blackbeanpartners.com/forms/send`

An example of including your `projectId` and `formName` in your form can be as follows.

```html
<input type="hidden" name="formName" value="contactUs" />
<input type="hidden" name="projectId" value="blackbean" />
```

### Validating form data

On submission of a form, you should receive a POST with an HTTP Response code `200` upon submission. If you receive codes such as a `422` then it means there was an error processing the form and can be found under the `error` field in the response.

When a form is successfully submitted, you will be able to find it under `forms` inside of your CMS.

### Frequently Asked Questions

#### Why are my files not being submitted?

We currently **do not** support any form of uploading that requires form data's encoding type to be `multipart/form-data`