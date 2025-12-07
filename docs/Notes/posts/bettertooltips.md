---
title: "MkDocs : Better Tooltips?"
date: 2025-12-07
hide:
    - toc
---

MkDocs already [supports tooltips](https://squidfunk.github.io/mkdocs-material/reference/tooltips/) natively. For example :

<!-- more -->

```markdown title="Markdown"
[Try hovering over this]("Hello, I'm a tooltip")
```

<div class="result" markdown>

[Try hovering over this]("Hello, I'm a tooltip")

</div>

### Make tooltips unclickable

The issue is that the tooltip is clickable and doing so will refresh the page. This is an unwanted function, but we can fix this by adding an appropriate attribute tag with the [Attribute Lists](https://python-markdown.github.io/extensions/attr_list/) extension. 

```markdown title="Markdown"
[Try hovering over this]("Hello, I'm a tooltip"){: onclick="this.blur(); return false;"}
```

<div class="result" markdown>

[Try hovering over this]("Hello, I'm a tooltip"){: onclick="this.blur(); return false;"}

</div>

### Bigger tooltips

While this may be satisfactory, what if I want an even bigger tootlip? What if I want to select and copy something from the tooltip? There is a workaround with MkDocs' [instant preview](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/?h=instant+preview#instant-previews). The idea is that we create a separate markdown file for our tooltips :

````markdown title="tooltips.md"
# Tooltips

### Example tooltip

This is an example tooltip. You can now select and copy text from the tooltip. You can even add lists, sample code, etc...

- item 1
- item 2
- item 3

```python
text = "Example Code"
print(test)
```

### Another Tooltip

Lorem Ipsum ...
````

Whenever we want to bring up this tooltip, we can just add a link to this markdown file at the corresponding header and add the `data-preview` attribute :

```markdown title="Markdown"
[Example Tooltip](../../hidden/tooltips.md#example-tooltip){: data-preview }

[Another Tooltip](../../hidden/tooltips.md#another-tooltip){: data-preview }
```

<div class="result" markdown>

[Example Tooltip](../../hidden/tooltips.md#example-tooltip){: data-preview }

[Another Tooltip](../../hidden/tooltips.md#another-tooltip){: data-preview }

</div>

Clicking on the tooltips above brings us to the page associated with `tooltips.md` but in many cases that is unnecessary. We can remove this functionality by attaching the `onclick="this.blur(); return false;"` attribute which we used earlier.

```markdown title="Markdown"
[Another Tooltip](../../hidden/tooltips.md#another-tooltip){: onclick="this.blur(); return false;" data-preview }
```

<div class="result" markdown>

[Another Tooltip](../../hidden/tooltips.md#another-tooltip){: onclick="this.blur(); return false;" data-preview }

</div>