# obtain_view

## URL format

http://root/obtain_view/{{design_document}}/{{view}}/{{key}}?secondaryParam=value

Where design_document is the name of the document containing the view we want to return,
view is the name of the view within that design document to access and key is the key to pass to the view.

This may need expanded to allow for multiple keys.

## Response Format

{

    "documents":[]

}
