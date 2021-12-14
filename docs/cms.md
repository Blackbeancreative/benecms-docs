# CMS / Editor

### Table of Contents
- [Documents](#documents)
    - [Creating a document](#creating-a-document)
    - [Modifying a document](#modifying-a-document)
    - [Drafting](#drafting)
- [Editors](#editors)
    - [Adding an editor](#adding-an-editor)
    - [Assigning roles](#assigning-roles)
    - [Frequently Asked Questions](#frequently-asked-questions)
- [Collections](#collections)
    - [Creating a collection](#creating-a-collection)
- [Tags](#tags)
    - [Creating a tag](#creating-a-tag)
    - [Tagging a document](#tagging-a-document)
- [Schemas](#schemas)
    - [Creating a schema](#creating-a-schema)
    - [What are widgets?](#what-are-widgets)
        - [List of Widgets](#list-of-widgets)
- [DataStore](#datastore)
- [Users](#users)
    - [Creating a user](#creating-a-user)
    - [Modifying a user](#modifying-a-user)


## Documents

### Creating a document

For creating a document, make sure your document is clearly titled. The slug will be pre-generated based off of the title.

You can create your document by accessing the collection that you want your Document to be stored.

**NOTE:** You must have a schema created for your Document.

### Modifying a document

All documents can be modifiable and your content validation will be built in as it is being provided by the Schema

### Drafting

You can set your document into Drafting mode, this will hide the Document from being publicized unless the Developer uses `?preview=true` at the end of the REST API.

## Editors

### Adding an Editor

Creating an editor is a very simple process that only requires knowing the email address of the editor and understanding what role you would like to give your Editor.

On creation of the Editor, they will be sent an email containing a temporary pass that will be mandatory change upon login.

### Assigning Roles

Giving an editor specific roles will help yourself and help the Editor not have more access than they need. A general content editor will likely never have the need to modify Schema or Collection content but allowing them access can create confusion and lead to potential misuses of content managing.

**Content / Documents** will only allow the Editor to modify data inside of a Document.

**Collections and Tags** will allow the Editor to modify Content / Documents and modify Documents that are inside of a collection as well as modify the Collection itself. **As of July 29th, 2021** this role will now allow you to modify and manage Tags.

**Collections, Tags and Schemas** will allow the Editor to modify Content / Documents and modify anything belonging to Collections and Schemas. This role should mainly be assigned to someone who either knows what they are doing or is a **developer**.

**Manager** will give full access to allow modification of any form of data including the addition / deletion of Editors.

### Frequently  Asked Questions

#### Modifying Roles

As of right now, the **only way** to change the roles of an editor is to remove their account and re-create it with the new permissions.

This is done for security reasons of the Editor.

#### Changing Information

As of right now, the **only way** to change the information of an editor is to remove their account and re-create it with the new permissions.

This is done for security reasons of the Editor.

## Collections

Collections is an organization place where your documents will be stored. You can imagine a simple layout being like follows.

For a blogging site, we'd like to have data separated between posts and the pages themselves. If we wanted a Home page, about page and wanted to have separate content for example. However by separating data into Collections (such as Blogs) it allows us to have all blog posts in one area which can be useful if we ever make a "Blogs" page where Developers can easily cycle through that data.

```
Collections
-- Pages
---| Home
---| About
-- Blogs
---| My first blog
---| My second blog
---| My third blog
```

### Creating a collection

For creating a collection, make sure your collection name has no spaces (any spaces will be replaced with "_").

You can create your collection by accessing "Manage Collections" inside of the Collections menu in the side bar.

## Tags

Tags is a way of assigning different documents to different categories beyond their collections. This could be useful as a means of organizing blog posts into sub-categories behind just a "Blogs" or "Posts" collection.

Documents **can be multi-tagged** meaning they can have more than one tag associated to them.

### Creating a tag

For creating a tag, make sure your tagname has no spaces (any spaces will be replaced with "_").

You can create your tag by accessing "Manage Tags" inside of the Tags menu in the side bar.

### Tagging a document

When accessing a Document, on the right hand side you will see a dropdown that allows you the ability to select different tags. When tagging a document, a pill-styled label will appear below the dropdown meaning the Document can be pulled from that tag specifically.

## Schemas

Schematics are the "structure" and "order" of how certain fields are laid out for your Documents. If you have a blog post then having schema fields such as "thumbnail" or "title" are more appropriate for a blog rather. Whereas you wouldn't use that for things such as a Frequently Asked Questions page.

### Creating a schema

For creating a schema, make sure your schema name has no spaces (any spaces will be replaced with "_").

You can create your schema by accessing "Manage Schemas" inside of the Schemas menu in the side bar.

### What are widgets?

Widgets are different types of fields that are used for your Document to allow you to bring more structure in what form of data you would like to see.

If you add a `select` widget, then you will only want to add dropdown elements with values to them where as a `string` or `text` widget allows you to put any form of text either in a single line or multiline editor.

#### List of Widgets

##### String

- Will only show a single line for placing text.
- Useful for titles and other shorter types of content.

##### Text

- Will show one or more lines for placing text.
- Useful for descriptions or larger areas of content.

##### List

- Will show a single line for playing text with options to add another line.
- Useful for stuff like adding "perks" or "specials" to a document.
    - Other examples can be something as simple as a "Message of the Day."

##### Markdown

- Will show one or more lines for placing text.
- Useful for descriptions or large areas of content.
- Features a rich editor allowing to add bolds, headings and other customization inside of the text block.

##### Number

- Will only show a single line for placing text.
- Any non-numeric number will not be added in the field.

##### Image

- Shows a selection screen for images
    - You can upload and manage images through here.
    - You can also manage media and other content through the "Media" option on the side bar.

##### Select

- Shows a dropdown that allows you to select one option
    - Useful if you want editors to only be able to select an option rather than type it out

##### Multiple

- Shows a dropdown that allows you to select *multiple* options
    - Useful if you want Editors to have the ability to select one *or more* options

##### Boolean

- Shows a select dropdown that only allows the answer to be "True" or "False"

##### Reference

- Allows referencing of different types of collections
    - Let's say you had a Products collection and wanted to list a Product inside of your Document. You would select your "Products" collection as the Schema value and the editor will have a choice of which product that wants to be embedded in the document.
    - Very useful if you want to assign different forms of content to different documents.

##### DataStore 

- Allows referencing of values inside of DataStore

##### Object

- Creates a schema field inside of the current field
    - Useful for organizing fields within the Document itself.

## Data Store

DataStore is a basic data storing convention consisting of "key, value" data. These are essentially used for storing basic types of information that might be universally across all documents or are just general values stored site-wide (such as a site title, site name, company phone number).

## Users

Users are a way that customers/consumers can potentially access a gated portion of your website. We have support for custom-made roles (through the Console interface).

**Note: In order to enable this feature, your project manager must enable Users in the Project Settings**

### Creating a user

Creating a user is a very simple process that only requires knowing the email address of the user and understanding what role you would like to give them (if roles are provided by the Project Manager).

Once a user is created, they will be emailed a generated password to login.

### Modifying a user

Due to **security reasons** the only abilities to modify a user are by outright deleting it or modifying their internal datastore value. This is typically something you should not want to mess with unless absolutely necessary.