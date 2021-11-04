# Schemas

## What are schemas?

Schematics are the "structure" and "order" of how certain fields are laid out for your Documents. If you have a blog post then having schema fields such as "thumbnail" or "title" are more appropriate for a blog rather. Whereas you wouldn't use that for things such as a Frequently Asked Questions page.

## Creating a schema

For creating a schema, make sure your schema name has no spaces (any spaces will be replaced with "_").

You can create your schema by accessing "Manage Schemas" inside of the Schemas menu in the side bar.

## What are widgets?

### General

Widgets are different types of fields that are used for your Document to allow you to bring more structure in what form of data you would like to see.

If you add a `select` widget, then you will only want to add dropdown elements with values to them where as a `string` or `text` widget allows you to put any form of text either in a single line or multiline editor.

### List of Widgets

#### String

- Will only show a single line for placing text.
- Useful for titles and other shorter types of content.

#### Text

- Will show one or more lines for placing text.
- Useful for descriptions or larger areas of content.

#### List

- Will show a single line for playing text with options to add another line.
- Useful for stuff like adding "perks" or "specials" to a document.
    - Other examples can be something as simple as a "Message of the Day."

#### Markdown

- Will show one or more lines for placing text.
- Useful for descriptions or large areas of content.
- Features a rich editor allowing to add bolds, headings and other customization inside of the text block.

#### Number

- Will only show a single line for placing text.
- Any non-numeric number will not be added in the field.

#### Image

- Shows a selection screen for images
    - You can upload and manage images through here.
    - You can also manage media and other content through the "Media" option on the side bar.

#### Select

- Shows a dropdown that allows you to select one option
    - Useful if you want editors to only be able to select an option rather than type it out

#### Multiple

- Shows a dropdown that allows you to select *multiple* options
    - Useful if you want Editors to have the ability to select one *or more* options

#### Boolean

- Shows a select dropdown that only allows the answer to be "True" or "False"

#### Reference

- Allows referencing of different types of collections
    - Let's say you had a Products collection and wanted to list a Product inside of your Document. You would select your "Products" collection as the Schema value and the editor will have a choice of which product that wants to be embedded in the document.
    - Very useful if you want to assign different forms of content to different documents.

#### DataStore 

- Allows referencing of values inside of DataStore

#### Object

- Creates a schema field inside of the current field
    - Useful for organizing fields within the Document itself.