---
title: about
layout: page
permalink: /about
---

This is an example of a page. 

New pages can be created in the `_pages` directory with the following frontmatter:

```markdown
---
title: about
layout: page
permalink: /about
---
```

Then, you can modify `navigation.html` in `_includes` to include this new page in the header:

```html
<li><a href="{{ site.baseurl }}/about">about</a></li>
```