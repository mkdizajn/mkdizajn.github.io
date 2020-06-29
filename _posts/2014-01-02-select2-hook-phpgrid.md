---
layout: post
title: Select2 hook to trigger phpgrid
published: true
tags:
  - selec2
  - phpgrid
  - javascript
---

<div class="message">
  Hi! This is an example code post that shows several types of great select2 content via ajax search and redirecting result from outside (this) scope :)
</div>

### Select2 hook on phpGrid

{% highlight js %}
$('.FormElement.select2').select2({
    width: '99%',
    separator: ';',
    placeholder: "-- Select --",
    minimumInputLength: 1,
    allowClear: true,
    dropdownCssClass: "malaslova",

    initSelection: function(element, callback) {
        var res = "";
        var tmp = "";

        if (element.attr('temp') == undefined) { 
            tmp = element.val().split(':')[0].trim();
            element.attr('temp', tmp); 
        }

        tmp = element.attr('temp');

        res = {
            id: tmp,
            text: element.val()
        };
        callback(res);
    },

    ajax: {
        url: "/main/ajax/lookup_select2.php",
        dataType: 'json',
        quietMillis: 750,
        data: function(term) {
            return {
                lookup_table: $(this).attr('rel'),
                lookup_key: $(this).attr('lookup_key'), 
                id_table_main: $('.selected_tab_parent').attr('rel'),
                fkid: $('.selected_tab_parent').attr('node_id'),
                q: term,
                mod: window.modtype
            };
        },
        results: function(data) {
            var results = [];
            var id1 = data.id;
            var name = data.text;
            $.each(data.data, function(index, item) {
                results.push({
                    id: item[id1],
                    text: item[name].trim() + ' : ' + item[id1]
                });
            });
            return {
                results: results
            };
        }
    },

});
{% endhighlight %}

phpGrid has builtin form that have basic lookup feature, and in this gist I'm showing couple of methods that I do on aftershowform event.

* Hiding / Showing controls that have dependance of other controls
* Redirecting result value from one select2 to another
* Getting / setting multiselect for column
* Getting / setting form column count

cheers, k
