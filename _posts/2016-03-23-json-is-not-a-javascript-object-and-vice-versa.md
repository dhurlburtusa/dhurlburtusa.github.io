---
layout: post

doc:
  html:
    head:
      cls: no-js  Doc  Doc--blog  Doc--blog--jsonIsNotAJavaScriptObjectAndViceVersa
      title: JSON is not a JavaScript Object and Vice Versa - Blog - DH

author: Danny Hurlburt
#date: 2016-03-23 07:00:00
tags: json javascript
title: JSON is not a JavaScript Object and Vice Versa
---

[<abbr title="JavaScript Object Notation">JSON</abbr>][JSON] is not a [JavaScript][] (JS) object, and a JS object is
not JSON.  JSON is a text-based (as opposed to binary) <q cite="http://www.json.org/">data-interchange format</q> much
like [YAML][] and [XML][], among others.  That is, it is nothing more than a string with a particular syntax.  JSON's
*syntax* **looks** like the *syntax* of a [JS object literal][JsObjLit], but JSON *is* **not** a JS object.
<!-- stop excerpt -->
A JS object exists in a JS execution context.  JSON, on the other hand, exists where a string of characters is
allowed.  This can be over the network in an HTTP response, it can be in a text file, it can be a string in a
programming language.

## Similar but Different Syntax

The JSON syntax is similar to JS object literal syntax.  However, the JSON syntax is only a subset of the JS object
literal syntax.

Strict JSON requires that each name (aka key) is double quoted.  (Lenient JSON parsers accept un-quoted names.)

    { "name": "value" }

JavaScript doesn't have this restriction.

    var obj = { name: "value" };

JSON is limited in what the value may be.  The value in JavaScript may be any value including `undefined`, a
`function`, Date objects, other objects, special values like `NaN`, etc.  JSON is limited to `null`, numbers, boolean,
strings, arrays, and other JSON objects.

For instance, take the following JavaScript object.

    var person = {
        first_name: "Dan",
        last_name: "Hurlburt",
        full_name: function () {
          return this.first_name + " " + this.last_name;
        },
        dob: new Date(12345678),
        is_us_citizen: true,
        ssn: NaN
      };

It can't be converted to an equivalent JSON string.  About the best we can do is something like the following.

    {
      "first_name": "Dan",
      "last_name": "Hurlburt",
      "full_name": "Dan Hurlburt",
      "dob": "1970-01-01T03:25:45.000Z",
      "is_us_citizen": true,
      "ssn": null
    }

Some information has been lost.  The `full_name` name is no longer a function.  The `dob` is now a string that will
need to be parsed to turn it back into the equivalent JS Date.  The `ssn` is `null` instead of representing the
special `NaN` value.  It could have been serialized in JSON as `'NaN'` string but the JSON will need to be post
processed to change it back to `NaN`.

## JSON in JavaScript

Since JSON is nothing more than a **string** with a particular syntax, JSON can be embedded in JavaScript as a JS
String.

    var json = '{ "name": "value" }';

It is, however, misleading to call a variable in JavaScript `json` when it is a JS object.

    var json = { name: "value" };   // Misleading

It would not be misleading to call a variable in JavaScript `json` when it is a JS String that _conforms_ to the
JSON syntax.  See first example above.

A JavaScript object `obj` can be converted to JSON using [`JSON.stringify`][JsonStringify].

    var obj = { name: "value" };
    var json = JSON.stringify(obj);


## Drive the Point Home

YAML, another text data format, _can_ be used to *represent* the same data represented by JSON.  The difference being
that each data format will use a different syntax to represent the same data.

Here is JSON representing a person.

    {
      "first_name": "Dan",
      "last_name": "Hurlburt"
    }

Here is YAML representing the same person.

    first_name: Dan
    last_name: Hurlburt

Here is a JS object literal representing the same person.

    var person = {
      first_name: "Dan",
      last_name: "Hurlburt"
    };

Although all snippets above represent the same data, JSON is not a JS object and YAML is not a JS object.  However,
JSON and YAML can be parsed to generate the same JS object.

    var personJson = '{ "first_name": "Dan", "last_name": "Hurlburt" }';
    var person = JSON.parse(personJson);

    var personYaml = 'first_name: Dan\nlast_name: Hurlburt';
    var person = jsyaml.load(personYaml); // Assuming JS-YAML library available.

## Summary

JSON is not the same as a JS object.  A JS object is not the same as JSON.  The only relation between the two is that
they have overlapping syntax.  JSON, like other text-based data-interchange formats, is just a string will a
particular syntax.

[JavaScript]: https://developer.mozilla.org/en-US/docs/Web/JavaScript
[JsObjLit]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals
[JSON]: http://www.json.org/
[JsonStringify]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[XML]: https://www.w3.org/XML/
[YAML]: http://yaml.org/
