---
layout: post
title: Select2 hook to trigger phpgrid
published: true
tags: 
  - first
  - second
  - mirko
---

<div class="message">
  Hi! This is an example code post that shows several types of great select2 content via ajax search and redirecting result from outside (this) scope :)
</div>

### Select2 hook on phpGrid

{% highlight js %}
$('.FormElement.select2').select2({
    width: '99%',
    separator: ';', // naos separator, defaultni je ','
    placeholder: "-- Select --",
    minimumInputLength: 1,
    allowClear: true,
    dropdownCssClass: "malaslova",

    // init ili prvi puta samo se poziva!
    initSelection: function(element, callback) {
        var res = ""; // var za placeholder
        var tmp = ""; // var za prijenos

        if (element.attr('temp') == undefined) { // OVO JE SAMO PRVI PUTA!!!
            tmp = element.val().split(':')[0].trim(); // SAMO ID!
            element.attr('temp', tmp); // kopira init vrijednost u temp attr
            // element.val( element.attr("lookup_key") );
        }

        tmp = element.attr('temp');

        res = {
            id: tmp, //koristimo preneseni izraz koji izgleda kao id : text t.d. je nepromijenjen
            text: element.val()
        };
        // console.dir(res);
        callback(res);
    },

    // ovo samostalno radi za pretragu i ide upit prema server!
    ajax: {
        url: "/main/ajax/lookup_select2.php",
        dataType: 'json',
        quietMillis: 750,
        data: function(term) {
            return {
                lookup_table: $(this).attr('rel'),
                lookup_key: $(this).attr('lookup_key'), //.split('(')[1].slice(0,-1),
                id_table_main: $('.selected_tab_parent').attr('rel'), //+'_parentx',
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

}); // SELECT2 END
{% endhighlight %}

phpGrid has builtin form that have basic lookup feature, and in this gist I'm showing couple of methods that I do on aftershowform event.

* Hiding / Showing controls that have dependance of other controls
* Redirecting result value from one select2 to another
* Getting / setting multiselect for column
* Getting / setting form column count

cheers, k