<%*
let coreDefinition = await tp.system.prompt("What are you exploring?");

// Extract tag and replace spaces with hyphens
let extractedTag = coreDefinition.includes('-') 
  ? coreDefinition.split('-')[0].trim().split(' ').join('-')
  : coreDefinition.trim().split(' ').join('-');
-%>
---
tags:
  - <% extractedTag.toLowerCase() %>
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---
**Defintion:**
<% coreDefinition %> - <%* tR += await tp.system.prompt("What is " + extractedTag + "?") %>

<!-- How does it work? (The Logic) %>? --> 
- <%* tR += await tp.system.prompt("How does it work? (The Logic)") %>

**Implementation / Syntax:**
```
<%*
let syntaxInput = await tp.system.prompt("Implementation / Syntax");
// Check if input contains "or" and split into multiple code blocks
if (syntaxInput.includes(" or ")) {
  let syntaxParts = syntaxInput.split(" or ");
  syntaxParts.forEach((part, index) => {
    tR += part.trim();
    // Add newline and code fence for next block (except after last one)
    if (index < syntaxParts.length - 1) {
      tR += "\n```\n\n```\n";
    }
  });
} else {
  tR += syntaxInput;
}
%>
```

**Pitfalls:**
> <%* tR += await tp.system.prompt("The 'Gotcha' (Pitfalls)") %>

<%* 
// Rename LAST after all content is written
await tp.file.rename(extractedTag); 
-%>
