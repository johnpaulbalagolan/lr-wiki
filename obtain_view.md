# obtain_view

## URL format

    http://host/obtain_view/{{design_document}}/{{view}}/{{key}}?secondaryParam=value

Where design_document is the name of the document containing the view we want to return,
view is the name of the view within that design document to access and key is the key to pass to the view.

This may need expanded to allow for multiple keys.

> NB: if we internally add a discriminator to data service views, do we need to specify both?  Can we just create an internal view to lookup the views? or is that just too much overhead? @jimklo

> NB: how might we activate a list or show function against map/reduce? or is this described in some manner as part of config or some other convention?  Similarly how does this apply to reduction and grouping? Are secondaryParam's just undefined or is there some set of standard params that control the wrapper (pagination, max results, etc) and a passthrough param that forwards to views/list/show? @jimklo

## Response Format

    {
        "documents":[...]
    }