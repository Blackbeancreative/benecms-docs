# Developing with Bene

### Table of Contents
- [Using Restful API](#using-restful-api)
  - [URL Formatting](#url-formatting)
    - [Finding Tagged Content](#finding-tagged-content)
  - [Preview / Draft Mode](#preview-draft-mode)
  - [Accessing DataStore](#accessing-datastore)
  - [Development / Localhost](#development-localhost)
- [Using Forms API](#using-forms-api)
  - [Creating Forms](#creating-forms)
  - [Validating form data](#validating-forms-data)
  - [Frequently Asked Questions](#frequently-asked-questions)
- [Using Users API](#using-users-api)
  - [Special Note](#special-note)
  - [User Lifecycle](#user-lifecycle)
  - [Viewing Session](#session)
  - [Creation](#creation)
  - [Authentication](#login)
  - [Activation](#activate)
  - [Forgot My Password (Send Forgot)](#forgot-send-forgot)
  - [Forgot My Password (Validate & New Password)](#forgot-validate-amp-new-password)
  - [Updating a user](#update)
  - [Logging out a user](#logout)


## Using RESTFUL API

### URL Formatting

All REST endpoints must require `projectId` as this is the unique identifier to pull the correct documents.

Your `projectId` can be found in the Pinco Console as a "Unique Name".

**Example URL**

`https://api.benecms.com/rest/{projectId}/{collection}/{document}`

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

`https://api.benecms.com/rest/{projectId}/tagged/{name}`

### Preview / Draft Mode

All documents can be set to a "Draft" mode which will hide the document from being provided in any endpoint unless `?preview=true` is included in the endpoint.

This can be a useful feature especially if using a Preview mode built into your framework such as Next JS.

### Accessing DataStore

As of **November 4th, 2021** you can now create/modify basic key, value items for your project. They are globally accessed through the RESTful API. 

**Example URL**

`https://api.benecms.com/rest/{projectId}/datastore`

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
3. Your action (or if using ajax/fetch, endpoint) must be pointed towards: `https://api.benecms.com/forms/send`

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

## Using Users API

### Special Note

In order to fully utilize the Users feature, the project manager must enable the feature inside of their Project Settings in BeneCMS Console. It is also highly recommended that you modify the URL paths for Login, Redirect, Activation and Forgot/Recovery.

**If you also get stuck or need help**, check out our official example (using CRA) that utilizes the Users API here: https://github.com/blackbeancreative/benecms-authentication

### User Lifecycle

The way our User feature works is based off JWT tokens and is purely based to be intregated via a series of POST/GET requests. All cookies are stored through BeneCMS therefore you can keep your website mostly cookie-less.

### Session

In order to initialize the session, and initialize the `isSite` cookie to register. You must send a session request before you consider using Login, Register, Activate, Forgot and Update methods.

To get a users current session you must submit a GET request to `https://api.benecms.com/user/session?id=[projectId]` where `projectId` is replaced with the project identifier that you login to BeneCMS Manage with.

What this will do is assign a cookie called `isSite` which is where we can find a users session on that specific page. This was made in the event there is two sites that a user visits back to back that both rely on Bene CMS that we call **multi-sessioning**.

### Creation

**API Route**
`POST https://api.benecms.com/user/create` 

**Fields**
- emailAddress (Email Address)
- password (Password)
- projectId (Project Identifier via BeneCMS)

**Tips**
- Make sure `emailAddress` is validated with `type="email"` as well as adding additional regex as a confirmation email will be sent to this address on confirmation.
- All passwords are mandatory to be one uppercase, one lowercase, one number and one special character minimum.
- It is recommended to make `projectId` a hidden value that is not seen to the user.
- For password creation, add a secondary "confirm password" field to make sure passwords are matching.
- **If you are a Project Manager**, make sure you have **redirectUri** and **activateUri** filled out in the Project Settings found in BeneCMS Console.

### Login

**API Route**
`POST https://api.benecms.com/user/login` 

**Fields**
- emailAddress (Email Address)
- password (Password)
- projectId (Project Identifier via BeneCMS)

**Tips**
- All passwords are mandatory to be one uppercase, one lowercase, one number and one special character minimum.
- It is recommended to make `projectId` a hidden value that is not seen to the user.

### Activate

**API Route**
`POST https://api.benecms.com/user/activate` 

**Fields**
- emailAddress (Email Address)
- key (Activation Code)
- projectId (Project Identifier via BeneCMS)

**Tips**
- It is recommended to make `projectId` a hidden value that is not seen to the user.
- **If you are a Project Manager**, make sure you have **redirectUri** and **activateUri** filled out in the Project Settings found in BeneCMS Console.

### Forgot (Send Forgot)

**API Route**
`POST https://api.benecms.com/user/sendForgot` 

**Fields**
- emailAddress (Email Address)
- projectId (Project Identifier via BeneCMS)

**Tips**
- It is recommended to make `projectId` a hidden value that is not seen to the user.
- **If you are a Project Manager**, make sure you have **redirectUri** and **forgotUri** filled out in the Project Settings found in BeneCMS Console.

### Forgot (Validate & New Password)

**API Route**
`POST https://api.benecms.com/user/forgot` 

**Fields**
- emailAddress (Email Address)
- password (Password)
- key (Activation Code)
- projectId (Project Identifier via BeneCMS)

**Tips**
- All passwords are mandatory to be one uppercase, one lowercase, one number and one special character minimum.
- It is recommended to make `projectId` a hidden value that is not seen to the user.
- **If you are a Project Manager**, make sure you have **redirectUri** filled out in the Project Settings found in BeneCMS Console.

### Update

**API Route**
`POST https://api.benecms.com/user/update` 

**Fields**
- datastore (Stringify JSON)

**Tips**
- Datastore **must** be validated via JSON before being submitted, otherwise it will throw an error and may cause unexpected results.

### Logout (Validate & New Password)

**API Route**
`POST https://api.benecms.com/user/logout` 

**Tips**
- **If you are a Project Manager**, make sure you have **redirectUri** filled out in the Project Settings found in BeneCMS Console.