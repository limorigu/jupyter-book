# Special content blocks

A common use of directives and roles is to designate "special blocks" of your content.
This allows your to include more complex information such as warnings and notes, citations, and figures.
This section covers a few common ones.

## Notes, warnings, and other admonitions

Let's say you wish to highlight a particular block of text that exists slightly apart from the narrative of your page.
You can use the **`{note}`** directive for this.

For example, the following text:

````md
```{note}
Here is a note!
```
````

Results in the following output:

```{note}
Here is a note!
```

````{margin} A note on nesting
You can nest admonitions (and other content blocks) inside one another. For example:

:::{note}
Here's a note block inside a margin block
:::

See {ref}`markdown/nexting` for instructions to do this.
````

There are a number of similarly-styled blocks of text. For example, here is a `{warning}`
block:

`````{warning}
Here's a warning! It was created with:
````
```{warning}
```
````
`````

For a complete list of options, see [the `sphinx-book-theme` documentation](https://sphinx-book-theme.readthedocs.io/en/latest/reference/demo.html#admonitions).

### Blocks of text with custom titles

You can also choose the title of your message box by using the
**`{admonition}`** directive. For example, the following text:

````md
```{admonition} Here's your admonition
Here's the admonition content
```
````

Results in the following output:

```{admonition} Here's your admonition
Here's the admonition content
```

If you'd like to **style these blocks**, then use the `:class:` option. For
example:

`````{admonition} This admonition was styled...
:class: tip
Using the following pattern:
````
```{admonition} My title
:class: tip
My content
```
````
`````

(admonitions:colons)=
### New Style Admonitions

The admonition syntax above utilises the general [directives syntax](content:myst/directives).
This has the advantage of making it consistent with every other directive.
However, a big disadvantage is that, when working in any standard Markdown editor (or the Jupyter Notebook interfaces),
the text they contain will not render nicely as standard Markdown (for Markdown previews).

By enabling extended syntax in your `_config.yml`, you will gain access to an alternative syntax for admonitions:

```yaml
parse:
  myst_extended_syntax: true
```

The key differences is that, instead of back-ticks (`` ` ``), colons (`:`) are used,
and thus **the content renders as regular Markdown**.

For example:

```md
:::{note}
This text is **standard** _Markdown_
:::
```

:::{note}
This text is **standard** _Markdown_
:::

Similar to normal directives, these admonitions can also be nested:

```md
::::{important}
:::{note}
This text is **standard** _Markdown_
:::
::::
```

::::{important}
:::{note}
This text is **standard** _Markdown_
:::
::::

:::{note}
This syntax only supports a select subset of directives:

> admonition, attention, caution, danger, error, important, hint, note, seealso, tip and warning.
:::

These directives do **not** currently allow for parameters to be set, but you can add additional CSS classes to the admonition as comma-delimited arguments after the directive name.
Also, `admonition` can have a custom title.
For example:

```md
:::{admonition,warning} This *is* also **Markdown**
This text is **standard** _Markdown_
:::
```

:::{admonition,warning} This *is* also **Markdown**
This text is **standard** _Markdown_
:::

(content/toggle-admonitions)=
### Hiding the content of admonitions

You can also hide the body of your admonition blocks so that users must click
a button to reveal their content. This is helpful if you'd like to make a point
that isn't immediately visible to the user.

To hide the body of admonition blocks, add a "dropdown" class to them, like so:

````md
```{note}
:class: dropdown
The note body will be hidden!
```
````

results in:

```{note}
:class: dropdown
The note body will be hidden!
```

You can use this in conjunction with `{admonition}` directives to include your
own titles and stylings. For example:

````md
:::{admonition,dropdown,tip} Click the + sign to see what's inside
Here's what's inside!
:::
````

results in:

:::{admonition,dropdown,tip} Click the + sign to see what's inside
Here's what's inside!
:::

:::{important}
Admonition dropdowns require JavaScript to be enabled on the browser which they are viewed.
By contrast, the [dropdown directive](content/panels) below works purely *via* HTML+CSS.
:::

### Insert code cell outputs into admonitions

If you'd like to insert the outputs of running code *inside* admonition
blocks, we recommend using [Glue functionality](content:code-outputs:glue).
For example, we'll insert one of the outputs that was glued into the book from the [code outputs page](./code-outputs.md).

The below code:

````md
```{note}
Here's my figure:
{glue:figure}`sorted_means_fig`
```
````

generates:

```{note}
Here's my figure:
{glue:}`sorted_means_fig`
```

See [](content:code-outputs:glue) for more information on how to use Glue to insert your outputs directly into your content.

:::{tip}
To hide code input and output that generated the variable you are inserting, use the `remove_cell` tag.
See [](../interactive/hiding.md) for more information and other tag options.
:::

(content/panels)=
## Panels and Dropdowns

Jupyter Book now also integrates the [sphinx-panels](https://sphinx-panels.readthedocs.io) extension.
This allows you to add special blocks to your online content, for example:

````{panels}
Content of the left panel.

{badge}`example-badge,badge-primary`

---

```{link-button} content/panels
:text: Clickable right panel
:type: ref
:classes: stretched-link
```

````

```{dropdown} Click on me to see my content!
I'm the content which can be **anything** {fa}`check,text-success ml-1`

:::{note}
Even other blocks.
:::
```

Which was created from:

`````md
````{panels}
Content of the left panel.

{badge}`example-badge,badge-primary`

---

```{link-button} content/panels
:text: Clickable right panel
:type: ref
:classes: stretched-link
```

````

```{dropdown} Click on me to see my content!
I'm the content which can be **anything** {fa}`check,text-success ml-1`

:::{note}
Even other blocks.
:::
```
`````

(content/definition-lists)=

## Definition Lists

Definition lists are enabled by setting in your `_config.yml`:

```yaml
parse:
  myst_extended_syntax: true
```

Definition lists utilise the [markdown-it-py deflist plugin](https://markdown-it-py.readthedocs.io/en/latest/plugins.html), which itself is based on the [Pandoc definition list specification](http://johnmacfarlane.net/pandoc/README.html#definition-lists).

This syntax can be useful, for example, as an alternative to nested bullet-lists:

- Term 1
  - Definition
- Term 2
  - Definition

Using instead:

```md
Term 1
: Definition

Term 2
: Definition
```

Term 1
: Definition

Term 2
: Definition

From the [Pandoc documentation](https://pandoc.org/MANUAL.html#definition-lists):

> Each term must fit on one line, which may optionally be followed by a blank line, and must be followed by one or more definitions.
> A definition begins with a colon or tilde, which may be indented one or two spaces.

> A term may have multiple definitions, and each definition may consist of one or more block elements (paragraph, code block, list, etc.)

Here is a more complex example, demonstrating some of these features:

Term *with Markdown*
: Definition [with reference](content/definition-lists)

  A second paragraph
: A second definition

Term 2
  ~ Definition 2a
  ~ Definition 2b

Term 3
:     A code block
: > A quote
: A final definition, that can even include images:

  <img src="../images/fun-fish.png" alt="fishy" width="200px">

This was created from:

```md
Term *with Markdown*
: Definition [with reference](ontent/definition-lists)

  A second paragraph

Term 2
  ~ Definition 2a
  ~ Definition 2b

Term 3
:     A code block

: > A quote

: A final definition, that can even include images:

  <img src="../images/fun-fish.png" alt="fishy" width="200px">
```

## Quotations and epigraphs

Quotations and epigraphs provide ways to highlight information given by others.
They behave slightly differently.

**Regular quotations** are controlled with standard markdown syntax, i.e., by
putting a caret (`>`) symbol in front of one or more lines of text. For example,
the following quotation:

> Here is a cool quotation.
>
> From me, Jo the Jovyan

Was created with this text:

```md
> Here is a cool quotation.
>
> From me, Jo the Jovyan
```

**Epigraphs** draw more attention to a quote and highlight its author. You should
keep these relatively short so that they don't take up too much vertical space. Here's
how an epigraph looks:

```{epigraph}
Here is a cool quotation.

From me, Jo the Jovyan
```

Was generated with this markdown:

````md
```{epigraph}
Here is a cool quotation.

From me, Jo the Jovyan
```
````

You can provide an **attribution** to an epigraph by adding `--` to the final line, followed
by the quote author. For example:

```{epigraph}
Here is a cool quotation.

-- Jo the Jovyan
```

Was generated with this markdown:

````md
```{epigraph}
Here is a cool quotation.

-- Jo the Jovyan
```
````

## Glossaries

Glossaries allow you to define terms in a glossary, and then link back to the
glossary throughout your content. You can create a glossary with the following
syntax:

````md
```{glossary}
term one
  An indented explanation of term 1

A second term
  An indented explanation of term2
```
````

which creates:

```{glossary}
term one
  An indented explanation of term 1

A second term
  An indented explanation of term2
```

To reference terms in your glossary, use the `{term}` role. For example,
`` {term}`term one` `` becomes {term}`term one`. And `` {term}`A second term` ``
becomes {term}`A second term`.

## Citations and cross-references

You can add citations and cross-references to your book's content. See
{doc}`citations` for more information.

## Figures

You can control many aspects of figures in your book. See {doc}`figures` for
more information.

## Page layout and sidebar content

You can also use MyST to control various aspects of the page layout. For more
information on this, see {doc}`layout`.

## Footnotes

You can include footnotes in your book's content using a standard markdown syntax.
This will include a numbered reference to the footnote in-line, and insert the footnote
to a list of footnotes at the bottom of the page.

To create a footnote, first insert a reference in-line with this syntax: `[^mylabel]`.
Then, define the text for that label like so:

```md
[^mylabel]: My footnote text.
```

You can define `[^mylabel]` anywhere in the page, though its definition will always
be placed at the bottom of your built page. For example, here's a footnote [^mynote]
and here's another one [^mynote2]. You can click either of them to see the footnotes
at the bottom of this page.

[^mynote]: Here's the text of my first note.
[^mynote2]: And the text of my second note.
            Note that
            [you can include markdown footnote definitions](https://executablebooks.org).
