# Attachments

In a lot of cases you have to make sure the signer retrieves attachments in addition to the main document to be sign. Don't worry, our signature API also supports attachments.

## Attachment format

The attachment must be a pdf file

## Attachment-types

When you upload an attachment you must decide which attachment-type you want to use. The default value is "show\_accept"

You can choose between 3 types of attachments:

| Type | Description | Remarks |
| :--- | :--- | :--- |
| show\_accept | The signer will see the attachment, and have to click a continue button before they get to the main document | Default value |
| read\_accept | The signer have to click on a checkbox to confirm that they have read and understood the attachment content | Coming soon |
| sign | The signer have to sign the attachment with the same signature method as the main document. | Coming soon&lt;br&gt;Extra cost per signature |

## Implementation guide

### Step 1 - Create document

Create the document as you usually would, with one change: mark the document with the number of attachments you want to include.

**Specify number of attachments in the create document request**

```text
{
   ...
   "Advanced": {    
    "Attachments": 2
  }
  ...
}
```

When you include attachments here, the document job will wait until all the attachments are uploaded before anyone is allowed to sign or notifications are sent out.

### Step 2 - Upload attachments

Read about the attachment endpoint [\[here\]\(https://developer.idfy.io/api\#operation/Attachments\_Create\)](https://github.com/idfy/docs/tree/9fb73e77ea2c6ea96df446df7b977361de545599/[here]%28https:/developer.idfy.io/api/README.md#operation/Attachments_Create%29)

Include the document id you retrieve in step one as a path parameter.

**Example attachment request**

```text
{

    "fileName": "Attachment1.pdf",
    "title": "Attachment 1 - Type description",
    "data": "Base 64 encoded pdf",
    "description": "This attachment describes bla bla bla...",
    "type": "show_accept",
    "signers": null

}
```

#### Requirements:

* The fileName must include the .pdf extension
* The data property must be a base64 encoded valid pdf

**Hint:**

If you only want some of the signers to retrieve an attachment; specify which in the signers property which is sat to null in the example above. The data type is a list with the signer id's you want to include.

### Step 3 - Result

When all the attachments are uploaded the document job will continue it's work and the document can be signed

### Application screenshots

![](../../.gitbook/assets/init.png)

![](../../.gitbook/assets/doc-overview-1.PNG)

![](../../.gitbook/assets/attach1.png)

![](../../.gitbook/assets/overview2.png)
