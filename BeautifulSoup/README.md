# CSS Selectors 

Here’s a comprehensive list of common CSS selectors along with their corresponding XPath expressions and examples. The XPath is provided so that it is easy for the reader to compare the two!

---

### 1. **Type Selector**
   - **CSS**: `element`
   - **Example**: `div`
   - **XPath**: `//div`
   - **Explanation**: Selects all `<div>` elements.

### 2. **ID Selector**
   - **CSS**: `#id`
   - **Example**: `#header`
   - **XPath**: `//*[@id='header']`
   - **Explanation**: Selects an element with the `id` attribute equal to `header`.

### 3. **Class Selector**
   - **CSS**: `.class`
   - **Example**: `.container`
   - **XPath**: `//*[contains(@class, 'container')]`
   - **Explanation**: Selects elements with a `class` attribute containing `container`.
   - ISSUE with the above mentioned statement!
        - The issue with `//*[contains(@class, 'fiction')]` is that `contains()` checks for any substring match within the `class` attribute. Therefore, it will match elements with classes like `"nonfiction"` as well, since `"fiction"` is a substring of `"nonfiction"`.

        - To specifically select elements with the class `fiction` and avoid matching `nonfiction`, you can use the following approach:

        - **Use Spaces to Match Whole Words**

            - You can use spaces around `fiction` to ensure it matches only whole words within the `class` attribute.

            ```xpath
            //*[contains(concat(' ', @class, ' '), ' fiction ')]
            ```

            - **Explanation**: `concat(' ', @class, ' ')` adds spaces before and after the `class` attribute value, so only exact matches (with spaces) are selected. This prevents partial matches like `"nonfiction"`.

            - Example

                Given the following HTML:
                ```html
                <div class="fiction">Fiction Book</div>
                <div class="nonfiction">Non-Fiction Book</div>
                <div class="science fiction">Science Fiction Book</div>
                ```

                - The XPath `//*[contains(concat(' ', @class, ' '), ' fiction ')]` would select:
                    - `<div class="fiction">Fiction Book</div>`
                    - `<div class="science fiction">Science Fiction Book</div>`

                    But it will not match:
                    - `<div class="nonfiction">Non-Fiction Book</div>`

### 4. **Universal Selector**
   - **CSS**: `*`
   - **Example**: `*`
   - **XPath**: `//*`
   - **Explanation**: Selects all elements in the document.

### 5. **Descendant Selector**
   - **CSS**: `ancestor descendant`
   - **Example**: `div p`
   - **XPath**: `//div//p` or `div/descendant::p`
   - **Explanation**: Selects all `<p>` elements that are descendants of `<div>` elements.

### 6. **Child Selector**
   - **CSS**: `parent > child`
   - **Example**: `ul > li`
   - **XPath**: `//ul/li` or `ul/child::li`
   - **Explanation**: Selects all `<li>` elements that are direct children of `<ul>` elements.

### 7. **Adjacent Sibling Selector**
   - **CSS**: `element1 + element2`
   - **Example**: `h1 + p`
   - **XPath**: `//h1/following-sibling::*[1][self::p]`
   - **Explanation**: Selects the first `<p>` element immediately following an `<h1>` element.

### 8. **General Sibling Selector**
   - **CSS**: `element1 ~ element2`
   - **Example**: `h1 ~ p`
   - **XPath**: `//h1/following-sibling::p`
   - **Explanation**: Selects all `<p>` elements that are siblings after an `<h1>` element.

### 9. **Attribute Selector**
   - **CSS**: `[attribute]`
   - **Example**: `[type]`
   - **XPath**: `//*[@type]`
   - **Explanation**: Selects all elements with a `type` attribute.

### 10. **Attribute Equals Selector**
   - **CSS**: `[attribute=value]`
   - **Example**: `[type="text"]`
   - **XPath**: `//*[@type='text']`
   - **Explanation**: Selects elements with a `type` attribute equal to `text`.

### 11. **Attribute Starts With Selector**
   - **CSS**: `[attribute^=value]`
   - **Example**: `[type^="te"]`
   - **XPath**: `//*[starts-with(@type, 'te')]`
   - **Explanation**: Selects elements with a `type` attribute starting with `te`.

### 12. **Attribute Ends With Selector**
   - **CSS**: `[attribute$=value]`
   - **Example**: `[type$="xt"]`
   - **XPath**: `//*[substring(@type, string-length(@type) - string-length('xt') + 1) = 'xt']`
   - **Explanation**: Selects elements with a `type` attribute ending with `xt`.

### 13. **Attribute Contains Selector**
   - **CSS**: `[attribute*=value]`
   - **Example**: `[type*="ex"]`
   - **XPath**: `//*[contains(@type, 'ex')]`
   - **Explanation**: Selects elements with a `type` attribute containing `ex`.

### 14. **First Child Pseudo-Class**
   - **CSS**: `:first-child`
   - **Example**: `p:first-child`
   - **XPath**: `*/p[1]`
   - **Explanation**: Selects the first `<p>` element among siblings.

### 15. **Last Child Pseudo-Class**
   - **CSS**: `:last-child`
   - **Example**: `p:last-child`
   - **XPath**: `*/p[last()]`
   - **Explanation**: Selects the last `<p>` element among siblings.

### 16. **Nth Child Pseudo-Class**
   - **CSS**: `:nth-child(n)`
   - **Example**: `li:nth-child(2)`
   - **XPath**: `*/li[2]`
   - **Explanation**: Selects the second `<li>` element among siblings.

### 17. **Only Child Pseudo-Class**
   - **CSS**: `:only-child`
   - **Example**: `p:only-child`
   - **XPath**: `*/p[count(preceding-sibling::*) = 0 and count(following-sibling::*) = 0]`
   - **Explanation**: Selects `<p>` elements that are the only child of their parent.

### 18. **First of Type Selector**
   - **CSS**: `:first-of-type`
   - **Example**: `p:first-of-type`
   - **XPath**: `//p[1]`
   - **Explanation**: Selects the first `<p>` element of its type within a parent.

### 19. **Last of Type Selector**
   - **CSS**: `:last-of-type`
   - **Example**: `p:last-of-type`
   - **XPath**: `//p[last()]`
   - **Explanation**: Selects the last `<p>` element of its type within a parent.

### 20. **Nth of Type Selector**
   - **CSS**: `:nth-of-type(n)`
   - **Example**: `li:nth-of-type(2)`
   - **XPath**: `//li[2]`
   - **Explanation**: Selects the second `<li>` element of its type within a parent.

### 21. **Empty Selector**
   - **CSS**: `:empty`
   - **Example**: `p:empty`
   - **XPath**: `//p[not(node())]`
   - **Explanation**: Selects `<p>` elements with no children (elements or text).

### 22. **Negation Pseudo-Class**
   - **CSS**: `:not(selector)`
   - **Example**: `p:not(.intro)`
   - **XPath**: `//p[not(contains(@class, 'intro'))]`
   - **Explanation**: Selects `<p>` elements that do not have the class `intro`.

---

This list includes some of the most common CSS selectors with equivalent XPath expressions. Note that while most CSS selectors can be converted to XPath, some require workarounds in XPath to achieve the same effect.

---

For better visualization, I present the above information in the form of a table.

| **Selector**                  | **CSS**                     | **Example**               | **XPath**                                                                                          | **Explanation**                                                                                              |
|-------------------------------|-----------------------------|---------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| **Type Selector**             | `element`                   | `div`                     | `//div`                                                                                           | Selects all `<div>` elements.                                                                                |
| **ID Selector**               | `#id`                       | `#header`                 | `//*[@id='header']`                                                                               | Selects an element with the `id` attribute equal to `header`.                                                |
| **Class Selector**            | `.class`                    | `.container`              | `//*[contains(concat(' ', @class, ' '), ' container ')]`                                          | Selects elements with `class` containing `container` as a whole word.                                        |
| **Universal Selector**        | `*`                         | `*`                       | `//*`                                                                                             | Selects all elements in the document.                                                                        |
| **Descendant Selector**       | `ancestor descendant`       | `div p`                   | `//div//p`                                                                                        | Selects all `<p>` elements that are descendants of `<div>` elements.                                         |
| **Child Selector**            | `parent > child`            | `ul > li`                 | `//ul/li`                                                                                         | Selects all `<li>` elements that are direct children of `<ul>` elements.                                     |
| **Adjacent Sibling Selector** | `element1 + element2`       | `h1 + p`                  | `//h1/following-sibling::*[1][self::p]`                                                           | Selects the first `<p>` element immediately following an `<h1>` element.                                     |
| **General Sibling Selector**  | `element1 ~ element2`       | `h1 ~ p`                  | `//h1/following-sibling::p`                                                                       | Selects all `<p>` elements that are siblings after an `<h1>` element.                                        |
| **Attribute Selector**        | `[attribute]`               | `[type]`                  | `//*[@type]`                                                                                      | Selects all elements with a `type` attribute.                                                                |
| **Attribute Equals Selector** | `[attribute=value]`         | `[type="text"]`           | `//*[@type='text']`                                                                               | Selects elements with a `type` attribute equal to `text`.                                                    |
| **Attribute Starts With**     | `[attribute^=value]`        | `[type^="te"]`            | `//*[starts-with(@type, 'te')]`                                                                   | Selects elements with a `type` attribute starting with `te`.                                                 |
| **Attribute Ends With**       | `[attribute$=value]`        | `[type$="xt"]`            | `//*[substring(@type, string-length(@type) - string-length('xt') + 1) = 'xt']`                    | Selects elements with a `type` attribute ending with `xt`.                                                   |
| **Attribute Contains**        | `[attribute*=value]`        | `[type*="ex"]`            | `//*[contains(@type, 'ex')]`                                                                      | Selects elements with a `type` attribute containing `ex`.                                                    |
| **First Child Pseudo-Class**  | `:first-child`              | `p:first-child`           | `*/p[1]`                                                                                          | Selects the first `<p>` element among siblings.                                                              |
| **Last Child Pseudo-Class**   | `:last-child`               | `p:last-child`            | `*/p[last()]`                                                                                     | Selects the last `<p>` element among siblings.                                                               |
| **Nth Child Pseudo-Class**    | `:nth-child(n)`             | `li:nth-child(2)`         | `*/li[2]`                                                                                         | Selects the second `<li>` element among siblings.                                                            |
| **Only Child Pseudo-Class**   | `:only-child`               | `p:only-child`            | `*/p[count(preceding-sibling::*) = 0 and count(following-sibling::*) = 0]`                        | Selects `<p>` elements that are the only child of their parent.                                              |
| **First of Type Selector**    | `:first-of-type`            | `p:first-of-type`         | `//p[1]`                                                                                          | Selects the first `<p>` element of its type within a parent.                                                 |
| **Last of Type Selector**     | `:last-of-type`             | `p:last-of-type`          | `//p[last()]`                                                                                     | Selects the last `<p>` element of its type within a parent.                                                  |
| **Nth of Type Selector**      | `:nth-of-type(n)`           | `li:nth-of-type(2)`       | `//li[2]`                                                                                         | Selects the second `<li>` element of its type within a parent.                                               |
| **Empty Selector**            | `:empty`                    | `p:empty`                 | `//p[not(node())]`                                                                               | Selects `<p>` elements with no children (elements or text).                                                  |
| **Negation Pseudo-Class**     | `:not(selector)`            | `p:not(.intro)`           | `//p[not(contains(@class, 'intro'))]`                                                             | Selects `<p>` elements that do not have the class `intro`.                                                   | 

---

# CSS Selectors representation in BeautifulSoup

Here’s how to represent each of the CSS selectors in **Beautiful Soup**:

| **Selector**                  | **CSS**                     | **Example**               | **Beautiful Soup Equivalent**                                                                 | **Explanation**                                                                                              |
|-------------------------------|-----------------------------|---------------------------|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| **Type Selector**             | `element`                   | `div`                     | `soup.find_all("div")`                                                                         | Selects all `<div>` elements.                                                                                |
| **ID Selector**               | `#id`                       | `#header`                 | `soup.find(id="header")`                                                                       | Selects an element with `id="header"`.                                                                       |
| **Class Selector**            | `.class`                    | `.container`              | `soup.find_all(class_="container")`                                                            | Selects elements with `class="container"`.                                                                   |
| **Universal Selector**        | `*`                         | `*`                       | `soup.find_all(True)`                                                                          | Selects all elements in the document.                                                                        |
| **Descendant Selector**       | `ancestor descendant`       | `div p`                   | `soup.select("div p")`                                                                         | Selects all `<p>` elements that are descendants of `<div>` elements.                                         |
| **Child Selector**            | `parent > child`            | `ul > li`                 | `soup.select("ul > li")`                                                                       | Selects all `<li>` elements that are direct children of `<ul>` elements.                                     |
| **Adjacent Sibling Selector** | `element1 + element2`       | `h1 + p`                  | `soup.select("h1 + p")`                                                                        | Selects the first `<p>` element immediately following an `<h1>` element.                                     |
| **General Sibling Selector**  | `element1 ~ element2`       | `h1 ~ p`                  | `soup.select("h1 ~ p")`                                                                        | Selects all `<p>` elements that are siblings after an `<h1>` element.                                        |
| **Attribute Selector**        | `[attribute]`               | `[type]`                  | `soup.select("[type]")`                                                                        | Selects all elements with a `type` attribute.                                                                |
| **Attribute Equals Selector** | `[attribute=value]`         | `[type="text"]`           | `soup.select('[type="text"]')`                                                                 | Selects elements with `type="text"`.                                                                         |
| **Attribute Starts With**     | `[attribute^=value]`        | `[type^="te"]`            | `soup.select('[type^="te"]')`                                                                  | Selects elements with a `type` attribute starting with `te`.                                                 |
| **Attribute Ends With**       | `[attribute$=value]`        | `[type$="xt"]`            | `soup.select('[type$="xt"]')`                                                                  | Selects elements with a `type` attribute ending with `xt`.                                                   |
| **Attribute Contains**        | `[attribute*=value]`        | `[type*="ex"]`            | `soup.select('[type*="ex"]')`                                                                  | Selects elements with a `type` attribute containing `ex`.                                                    |
| **First Child Pseudo-Class**  | `:first-child`              | `p:first-child`           | `soup.select("p:first-child")`                                                                 | Selects the first `<p>` element among siblings.                                                              |
| **Last Child Pseudo-Class**   | `:last-child`               | `p:last-child`            | `soup.select("p:last-child")`                                                                  | Selects the last `<p>` element among siblings.                                                               |
| **Nth Child Pseudo-Class**    | `:nth-child(n)`             | `li:nth-child(2)`         | `soup.select("li:nth-child(2)")`                                                               | Selects the second `<li>` element among siblings.                                                            |
| **Only Child Pseudo-Class**   | `:only-child`               | `p:only-child`            | `soup.select("p:only-child")`                                                                  | Selects `<p>` elements that are the only child of their parent.                                              |
| **First of Type Selector**    | `:first-of-type`            | `p:first-of-type`         | `soup.select("p:first-of-type")`                                                               | Selects the first `<p>` element of its type within a parent.                                                 |
| **Last of Type Selector**     | `:last-of-type`             | `p:last-of-type`          | `soup.select("p:last-of-type")`                                                                | Selects the last `<p>` element of its type within a parent.                                                  |
| **Nth of Type Selector**      | `:nth-of-type(n)`           | `li:nth-of-type(2)`       | `soup.select("li:nth-of-type(2)")`                                                             | Selects the second `<li>` element of its type within a parent.                                               |
| **Empty Selector**            | `:empty`                    | `p:empty`                 | `soup.select("p:empty")`                                                                       | Selects `<p>` elements with no children (elements or text).                                                  |
| **Negation Pseudo-Class**     | `:not(selector)`            | `p:not(.intro)`           | `soup.select("p:not(.intro)")`                                                                 | Selects `<p>` elements that do not have the class `intro`.                                                   |

---

### Usage in Beautiful Soup

1. **Finding Elements**: Use `soup.find()` and `soup.find_all()` for simpler selectors (like tag name, class, and ID).
2. **Using `select` for Complex Selectors**: `soup.select()` supports a variety of CSS selectors, including descendant, child, and sibling selectors, as well as attribute-based and pseudo-class selectors.

### Example Code

```python
from bs4 import BeautifulSoup

html_content = """
<div id="header">Header</div>
<div class="container">Main Content</div>
<div class="nonfiction">Nonfiction Book</div>
<div class="fiction">Fiction Book</div>
<ul><li>Item 1</li><li>Item 2</li></ul>
"""

# Parse HTML content
soup = BeautifulSoup(html_content, "html.parser")

# Example usage
print(soup.find("div"))  # Type selector
print(soup.find(id="header"))  # ID selector
print(soup.find_all(class_="container"))  # Class selector
print(soup.select("div p"))  # Descendant selector
print(soup.select("ul > li"))  # Child selector
```

Using `select()` in Beautiful Soup makes it easy to implement a wide range of CSS selectors directly.