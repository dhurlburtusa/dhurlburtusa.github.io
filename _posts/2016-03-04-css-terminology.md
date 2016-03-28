---
layout: post

doc:
  html:
    head:
      cls: no-js  Doc  Doc--blog  Doc--blog--cssTerminology
      title: CSS Terminology - Blog - DH
      style: |
        <style>
          .BNF { padding: 1rem; }
          .BNF { background: #F3F6FA; border: 1px solid #CCC; border-radius: 4px; }
          .BNF dt { float: left; width: 196px; padding-right: 4px; white-space: nowrap; }
          .BNF dt::after { content: ": "; }
          .BNF dd { overflow: auto; }
          .BNF dd:last-child { margin: 0; }

          .BNF .c { color: #888; }
          .BNF .k { color: #080; font-weight: bold; }
          .BNF .nv { color: #369; white-space: nowrap; }
          .BNF .o {}
          .BNF .p { color: #888; }
          .BNF .l,
          .BNF .s2 { background: #F3F6FA; color: #BD5A73; font-weight: bold; }

          .Figure--bnf figcaption { font-weight: bold; }
        </style>

author: Danny Hurlburt
date: 2016-03-04 07:00:00
tags: css
---

Knowing the standard terminology may help when learning CSS.
<!-- stop excerpt -->
The standard terminology is declared in the CSS specification.  But, how many people do you know want to read a
specification?  Below is a summary of the terminology of the most common components of a CSS document.

<h4>Terminology</h4>

The following code example is used to help declare the following definitions.

{% highlight css linenos %}
.Example {
  background: black;
  color: hotpink;
}
{% endhighlight %}

<dl>
  <dt>Rule Set</dt>
  <dd>The whole code example above is a single rule set (or rule for short).</dd>

  <dt>Declaration Block</dt>
  <dd>The <code>{</code> and <code>}</code> plus everything in between.</dd>

  <dt>Selector</dt>
  <dd>
    <code>.Example</code> is the selector.  The selector is the part of the rule that determines which elements the
    declarations will apply.
  </dd>

  <dt>Property Name</dt>
  <dd>
    <code>background</code> and <code>color</code> are each examples of a property name (or property for short).
  </dd>

  <dt>Property Value</dt>
  <dd>
    <code>black</code> is the property value for the <code>background</code> property.  <code>hotpink</code> is the
    property value for the <code>color</code> property.
  </dd>

  <dt>Declaration</dt>
  <dd>
    This is the combination of the property, the colon, the property value, and the semi-colon.  Therefore,
    <code>background: black;</code> is one declaration and <code>color: hotpink;</code> is another declaration.
  </dd>
</dl>

<h4>Selectors</h4>
<p>
  The selector in the above example is very simple.  However, selectors can become quite complex.  Although selectors
  have been around since the beginning of CSS, its terminology has changed over time.  (At the time of this writing),
  <a href="https://www.w3.org/TR/selectors4/#structure" target="css-spec">Selectors Level 4</a> uses what I believe to
  be the best terminology for selectors.
</p>
<p>
  The term selector can refer to a simple selector, compound selector, complex selector, or selector list.  A selector
  list is a comma-separated list of selectors.  A complex selector is a chain of one or more compound selectors
  separated by combinators.  A compound selector is a chain of simple selectors that are not separated by a combinator.
  It always begins with a type selector or a (possibly implied) universal selector.  No other type selector or universal
  selector is allowed in the sequence.  A simple selector is either a type selector, universal selector, attribute
  selector, class selector, ID selector, or pseudo-class.
</p>
<figure class="Figure--bnf">
  <figcaption>Selector Grammar</figcaption>
  <dl class="BNF">
    <dt>selector-list</dt>
    <dd>
      <span class="nv">&lt;complex-sel></span>
      <span class="p">[</span>
      <span class="l">,</span>
      <span class="nv">&lt;complex-sel></span>
      <span class="p">]</span>
      <span class="o">*</span>
    </dd>
    <dt>complex-sel</dt>
    <dd>
      <span class="nv">&lt;compound-sel></span>
      <span class="p">[</span>
      <span class="nv">&lt;combinator></span>
      <span class="nv">&lt;compound-sel></span>
      <span class="p">]</span>
      <span class="o">*</span>
    </dd>
    <dt>compound-sel</dt>
    <dd>
      <span class="p">[</span>
      <span class="nv">&lt;type-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;univ-sel></span>
      <span class="p">]</span>
      <span class="o">?</span>
      <span class="p">[</span>
      <span class="nv">&lt;attr-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;cls-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;id-sel></span>
      <span class="p">]</span>
      <span class="o">*</span>
      <span class="nv">&lt;pseudo-cls></span>
      <span class="o">*</span>
      <span class="nv">&lt;pseudo-el></span>
      <span class="o">?</span>
      <span class="nv">&lt;pseudo-cls-user-action></span>
      <span class="o">*</span>
    </dd>
    <dt>combinator</dt>
    <dd>
      <span class="s2">" "</span>
      <span class="o">|</span>
      <span class="l">></span>
      <span class="o">|</span>
      <span class="l">+</span>
      <span class="o">|</span>
      <span class="l">~</span>
      <span class="c">&nbsp;# With optional whitespace.</span>
    </dd>
    <dt>simple-sel</dt>
    <dd>
      <span class="nv">&lt;attr-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;cls-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;id-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-el></span>
      <span class="o">|</span>
      <span class="nv">&lt;type-sel></span>
      <span class="o">|</span>
      <span class="nv">&lt;univ-sel></span>
    </dd>
    <dt>attr-sel</dt>
    <dd>
      <span class="l">[</span>
      <span class="nv">&lt;attr-name></span>
      <span class="p">[</span>
      <span class="nv">&lt;attr-match></span>
      <span class="nv">&lt;attr-value></span>
      <span class="p">[</span>
      <span class="s2">" "</span>
      <span class="o">+</span>
      <span class="nv">&lt;attr-flags></span>
      <span class="p">]</span>
      <span class="o">?</span>
      <span class="p">]</span>
      <span class="o">?</span>
      <span class="l">]</span>
    </dd>
    <dt>attr-match</dt>
    <dd>
      <span class="l">=</span>
      <span class="o">|</span>
      <span class="l">~=</span>
      <span class="o">|</span>
      <span class="l">|=</span>
      <span class="o">|</span>
      <span class="l">^=</span>
      <span class="o">|</span>
      <span class="l">$=</span>
      <span class="o">|</span>
      <span class="l">*=</span>
    </dd>
    <dt>attr-value</dt>
    <dd>
      <span class="nv">&lt;ident></span>
      <span class="o">|</span>
      <span class="s2">"</span>
      <span class="nv">&lt;ident></span>
      <span class="s2">"</span>
    </dd>
    <dt>attr-flags</dt>
    <dd>
      <span class="k">i</span>
    </dd>
    <dt>cls-sel</dt>
    <dd>
      <span class="l">.</span
      ><span class="nv">&lt;cls-name></span>
    </dd>
    <dt>id-sel</dt>
    <dd>
      <span class="l">#</span
      ><span class="nv">&lt;id></span>
    </dd>
    <dt>pseudo-cls</dt>
    <dd>
      <span class="nv">&lt;pseudo-cls-dir></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-input></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-lang></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-link></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-matches></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-not></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-structural></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-target></span>
      <span class="o">|</span>
      <span class="nv">&lt;pseudo-cls-user-action></span>
    </dd>
    <dt>pseudo-cls-dir</dt>
    <dd>
      <span class="l">:dir</span
      ><span class="l">(</span>
      <span class="k">ltr</span>
      <span class="o">|</span>
      <span class="k">rtl</span>
      <span class="l">)</span>
    </dd>
    <dt>pseudo-cls-input</dt>
    <dd>
      <span class="l">:checked</span>
      <span class="o">|</span>
      <span class="l">:default</span>
      <span class="o">|</span>
      <span class="l">:enabled</span>
      <span class="o">|</span>
      <span class="l">:disabled</span>
      <span class="o">|</span>
      <span class="l">:indeterminate</span>
      <span class="o">|</span>
      <span class="l">:in-range</span>
      <span class="o">|</span>
      <span class="l">:invalid</span>
      <span class="o">|</span>
      <span class="l">:optional</span>
      <span class="o">|</span>
      <span class="l">:out-of-range</span>
      <span class="o">|</span>
      <span class="l">:read-only</span>
      <span class="o">|</span>
      <span class="l">:read-write</span>
      <span class="o">|</span>
      <span class="l">:required</span>
      <span class="o">|</span>
      <span class="l">:valid</span>
    </dd>
    <dt>pseudo-cls-lang</dt>
    <dd>
      <span class="l">:lang</span
      ><span class="l">(</span>
      <span class="nv">&lt;lang-list></span>
      <span class="l">)</span>
    </dd>
    <dt>pseudo-cls-link</dt>
    <dd>
      <span class="l">:link</span>
      <span class="o">|</span>
      <span class="l">:visited</span>
    </dd>
    <dt>pseudo-cls-matches</dt>
    <dd>
      <span class="l">:matches</span
      ><span class="l">(</span>
      <span class="nv">&lt;selector-list></span>
      <span class="l">)</span>
    </dd>
    <dt>pseudo-cls-not</dt>
    <dd>
      <span class="l">:not</span
      ><span class="l">(</span>
      <span class="nv">&lt;selector-list></span>
      <span class="l">)</span>
    </dd>
    <dt>pseudo-cls-structural</dt>
    <dd>
      <span class="l">:blank</span>
      <span class="o">|</span>
      <span class="l">:empty</span>
      <span class="o">|</span>
      <span class="l">:first-child</span>
      <span class="o">|</span>
      <span class="l">:first-of-type</span>
      <span class="o">|</span>
      <span class="l">:last-child</span>
      <span class="o">|</span>
      <span class="l">:last-of-type</span>
      <span class="o">|</span>
      <span class="l">:only-child</span>
      <span class="o">|</span>
      <span class="l">:only-of-type</span>
      <span class="o">|</span>
      <span class="l">:nth-child</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:nth-last-match</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="k">of</span>
      <span class="nv">&lt;selector-list></span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:nth-match</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="k">of</span>
      <span class="nv">&lt;selector-list></span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:nth-of-type</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:nth-last-child</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:nth-last-of-type</span
      ><span class="l">(</span>
      <span class="nv">A</span>
      <span class="nv">n</span>
      <span class="o">+</span>
      <span class="nv">B</span>
      <span class="l">)</span>
      <span class="o">|</span>
      <span class="l">:root</span>
      <span class="o">|</span>
      <span class="l">:user-error</span>
    </dd>
    <dt>pseudo-cls-target</dt>
    <dd>
      <span class="l">:target</span>
    </dd>
    <dt>pseudo-cls-user-action</dt>
    <dd>
      <span class="l">:active</span>
      <span class="o">|</span>
      <span class="l">:focus</span>
      <span class="o">|</span>
      <span class="l">:hover</span>
    </dd>
    <dt>pseudo-el</dt>
    <dd>
      <span class="l">::after</span>
      <span class="o">|</span>
      <span class="l">::before</span>
      <span class="o">|</span>
      <span class="l">::first-letter</span>
      <span class="o">|</span>
      <span class="l">::first-line</span>
    </dd>
    <dt>type-sel</dt>
    <dd>
      <span class="l">div</span>
      <span class="o">|</span>
      <span class="l">p</span>
      <span class="o">|</span>
      <span class="l">span</span>
      <span class="o">|</span>
      <span class="l">body</span>
      <span class="o">|</span>
      <span class="l">ul</span>
      <span class="o">|</span>
      <span class="l">li</span>
      <span class="o">|</span>
      <span class="l">td</span>
      <span class="c">&nbsp;# Etc.</span>
    </dd>
    <dt>univ-sel</dt>
    <dd>
      <span class="l">*</span>
    </dd>
  </dl>
</figure>

<p>
  See <a href="https://www.w3.org/TR/selectors4/#structure" target="css-spec">Selectors Level 4</a> for more details
  on selectors.
</p>

<!--
3.2. Determining the Subject of a Selector

The elements of a document tree that are represented by a selector are the subjects of the selector.

By default, the subjects of a selector are the elements represented by the last compound selector in the selector.
Thus a selector consisting of a single compound selector represents any element satisfying its requirements.

Prepending another compound selector and a combinator to a sequence imposes additional matching constraints, so the
subjects of the selector are always a subset of the elements represented by the last compound selector.

As a feature of the complete Selectors profile, the subject of the selector can be explicitly identified by prepending
an exclamation mark (!) to one of the compound selectors in a selector.  Although the element structure that the
selector represents is the same with or without the exclamation mark, indicating the subject in this way can change
which compound selector represents the subject in that structure.

Should the exclamation mark be prepended or appended to the subject?  Or both?  Or prepend two, to avoid the "! = not"
issue?

For example, the following selector represents a list item LI unique child of an ordered list OL:

OL > LI:only-child

However, the following one represents an ordered list OL having a unique child, that child being a LI:

!OL > LI:only-child

The tree structures represented by these two selectors are the same, but the subjects of the selectors are not.
-->

<h4>More Info</h4>
<p>
  See sections <a href="https://www.w3.org/TR/2011/REC-CSS2-20110607/syndata.html#rule-sets" target="css-spec">4.1.7</a>
  and <a href="https://www.w3.org/TR/2011/REC-CSS2-20110607/syndata.html#declaration" target="css-spec">4.1.8</a> in the
  CSS specification for more information on rule sets, selectors, declaration blocks, properties, property values, and
  declarations.
</p>

<h4>See Also</h4>
<ul>
  <li><a href="https://developer.mozilla.org/en-US/Learn/CSS/Introduction_to_CSS/Syntax" rel="exteranl" target="mdn_css_syntax">CSS Syntax</a></li>
</ul>
