#Backbone Editable#

This is an in place editor mixin written in coffeescript for a backbone view.

It defines a method for including mixins (```@mixin```, directly inspired by: https://github.com/jashkenas/coffee-script/issues/452#issuecomment-3699651) and the mixin itself Backbone.Mixin.Editable

This project was extracted from a rails app so usage instructions pertain to rails.
Starting in your project root, download the coffeescript file:

    cd vendor/assets/javascripts
    curl -C - -O https://raw.github.com/matthewsmart/backbone-editable/master/backbone_editable.js.coffee
    
Include the file in your javascript manifest file, after backbone, but before your backbone app:

    ...
    //= require underscore
    //= require backbone

    // Backbone Mixins
    //= require backbone_editable
    
    //= require appname
    ...

Finally, include the mixin in your view:

    class App.Views.MyView extends Backbone.View
      @mixin Backbone.Mixin.Editable
      
      initialize: (options = {}) ->
        @initEditable()
        # To redraw the model after changes
        # have been made.
        @model.on 'change', @render, this
      
      ...

*NOTE:* All model save events are silent by default. This can be changed
by calling ```@initEditable(silent_events: false)```. This setting can
be overridden on your editable by setting the data attribute
```data-silent='true'``` or ```data-silent='false'```

Now, to make a field in your template editable, regardless of your templating engine you need to set a class and some data attributes

To edit ```@model.get('options')[3].text:```

    <div class="editable" data-object="options" data-index="3" data-key="text">
      <%= @model.get('options')[3].text %>
    </div>
    
To edit ```@model.get('options').text:```

    <div class="editable" data-object="options" data-key="text">
      <%= @model.get('options').text %>
    </div>
    
To edit ```@model.get('options')[3]:```

    <div class="editable" data-object="options" data-index="3">
      <%= @model.get('options')[3] %>
    </div>
    
To edit ```@model.get('text')```

    <div class="editable" data-key="text">
      <%= @model.get('text') %>
    </div>
    
All of these fire a change event and save the model. If you tie render to your models change event, then the model will redraw with the new data.

### To be implemented soon
- Minimum/maximum text field width
- Silent changes

#### Pull Requests and suggestions welcome...
