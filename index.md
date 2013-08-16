---
title: Bootstrap Date/Time Picker
layout: layout
author: Thiago de Arruda
authorUrl: https://github.com/tarruda
projectName: bootstrap-datetimepicker
projectDescription: Date/Time Picker for Twitter Bootstrap 
zipDownloadUrl: assets/dist/bootstrap-datetimepicker-0.0.11.zip
githubUrl: https://github.com/tarruda/bootstrap-datetimepicker
css:
  - assets/css/bootstrap-datetimepicker.min.css
js:
  - assets/js/bootstrap-datetimepicker.min.js
  - assets/js/bootstrap-datetimepicker.pt-BR.js
  - assets/js/index.js
---
### Introduction
Simple date/time picker component based on the work of [Stefan Petre](http://www.eyecon.ro/bootstrap-datepicker/),
with contributions taken from [Andrew Rowls](https://github.com/eternicode) and
[jdewit](https://github.com/jdewit).

### Demo

####Default behavior in pt-BR, picks date/time with fast masked input typing (need only to type the numbers, the static part of the mask is inserted automatically if missing) or via the popup widget, which supports year, month, day, hour and minute views:

{% include demo1.html %}

Code:

{% highlight html %}
{% include demo1.html %}
{% endhighlight %}

####Similar to above example, but in US date/hour format:

{% include demo2.html %}

Code:

{% highlight html %}
{% include demo2.html %}
{% endhighlight %}

####Disables date picker:

{% include demo3.html %}

Code:

{% highlight html %}
{% include demo3.html %}
{% endhighlight %}

####Disables time picker:

{% include demo4.html %}

Code:

{% highlight html %}
{% include demo4.html %}
{% endhighlight %}

### API

The widget class provides 4 methods to manipulate dates:
'getDate'/'setDate' for working with UTC and 'getLocalDate'/'setLocalDate' for
working with local dates:

{% highlight js %}
// Considering you are on a GMT-3 timezone and the input contains '2000-01-17 10:00'
var localDate = picker.getLocalDate(); // localDate === 2000-01-17 07:00
var utcDate = picker.getDate(); // utcDate === 2000-01-17 10:00
//
picker.setLocalDate(new Date(1998, 10, 11, 4, 30)); // input === 1998-10-11 07:30
picker.setDate(new Date(Date.UTC(1998, 10, 11, 4, 30))); // input === 1998-10-11 04:30
{% endhighlight %}

The date value can be unset by passing 'null' to any of the 'set' methods or by
erasing the input:

{% highlight js %}
var picker = $('#datetimepicker'l).data('datetimepicker');
picker.setLocalDate(null);
// or
picker.setDate(null);
// or
input.val('');
input.change();
{% endhighlight %}

The only event exposed is 'changeDate', which will expose 'date' and
'localDate' properties on the event object:

{% highlight js %}
el.on('changeDate', function(e) {
  console.log(e.date.toString());
  console.log(e.localDate.toString());
});
{% endhighlight %}

### Options

These are the default options for initializing the widget:

{% highlight js %}
$.fn.datetimepicker.defaults = {
  maskInput: true,           // disables the text input mask
  pickDate: true,            // disables the date picker
  pickTime: true,            // disables de time picker
  pick12HourFormat: false,   // enables the 12-hour format time picker
  pickSeconds: true,         // disables seconds in the time picker
  startDate: -Infinity,      // set a minimum date
  endDate: Infinity          // set a maximum date
};
{% endhighlight %}

Examples of using these options can be seen in the file test/specs.coffee.

### Complete sample markup

Copy and paste the following code in a file(eg: test.html) and it should
produce a widget similar to the first demo:

{% highlight html %}
<!DOCTYPE HTML>
<html>
  <head>
    <link href="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.2.2/css/bootstrap-combined.min.css" rel="stylesheet">
    <link rel="stylesheet" type="text/css" media="screen"
     href="http://tarruda.github.com/bootstrap-datetimepicker/assets/css/bootstrap-datetimepicker.min.css">
  </head>
  <body>
    <div id="datetimepicker" class="input-append date">
      <input type="text"></input>
      <span class="add-on">
        <i data-time-icon="icon-time" data-date-icon="icon-calendar"></i>
      </span>
    </div>
    <script type="text/javascript"
     src="http://cdnjs.cloudflare.com/ajax/libs/jquery/1.8.3/jquery.min.js">
    </script> 
    <script type="text/javascript"
     src="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.2.2/js/bootstrap.min.js">
    </script>
    <script type="text/javascript"
     src="http://tarruda.github.com/bootstrap-datetimepicker/assets/js/bootstrap-datetimepicker.min.js">
    </script>
    <script type="text/javascript"
     src="http://tarruda.github.com/bootstrap-datetimepicker/assets/js/bootstrap-datetimepicker.pt-BR.js">
    </script>
    <script type="text/javascript">
      $('#datetimepicker').datetimepicker({
        format: 'dd/MM/yyyy hh:mm:ss',
        language: 'pt-BR'
      });
    </script>
  </body>
<html>
{% endhighlight %}

### Development

If you want to contribute, please follow the settings in the .lvimrc file (2
space indentation). 

To report bugs, ideally an automated test that reproduces the bug should be created in
 the 'test/issues.coffee' file(following the conventions of the tests already
defined there) and submitted with a pull request.

To compile/minify you need to have make, node.js and npm on your $PATH

{% highlight sh %}
$ git clone git://github.com/tarruda/bootstrap-datetimepicker.git
$ cd bootstrap-datetimepicker
$ make deps
$ make build
{% endhighlight %}

To run the automated tests:

{% highlight sh %}
$ make test
{% endhighlight %}

It should download all dependencies needed for testing(phantomjs, jquery...)

