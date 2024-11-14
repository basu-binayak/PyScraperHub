# XPath in detail

Let’s walk through **XPath** in detail with an example XML document. XPath (XML Path Language) is a query language for selecting and navigating nodes in an XML document. It is used widely to extract specific data from XML documents based on a structured path.

---
## Example XML Document

We’ll use an XML document that represents a bookstore inventory, with elements for books, authors, prices, and other details.

```xml
<bookstore>
    <book category="fiction" id="bk101">
        <title lang="en">The Great Gatsby</title>
        <author>F. Scott Fitzgerald</author>
        <price currency="USD">10.99</price>
        <year>1925</year>
    </book>
    <book category="nonfiction" id="bk102">
        <title lang="en">Sapiens</title>
        <author>Yuval Noah Harari</author>
        <price currency="USD">15.50</price>
        <year>2014</year>
    </book>
    <book category="fiction" id="bk103">
        <title lang="es">Cien años de soledad</title>
        <author>Gabriel Garcia Marquez</author>
        <price currency="EUR">12.30</price>
        <year>1967</year>
    </book>
    <book category="poetry" id="bk104">
        <title lang="en">The Sun and Her Flowers</title>
        <author>Rupi Kaur</author>
        <price currency="USD">13.50</price>
        <year>2017</year>
    </book>
</bookstore>
```

(Use <a href="https://codebeautify.org/Xpath-Tester">XPath Tester</a> to test the Xpath statements below!)


## XPath Syntax and Components

In XPath, expressions are used to navigate through elements and attributes in an XML document. Let’s go through the key components of XPath and how to apply them to this XML document.

### 1. **Selecting Nodes**

- **Root Node (`/`)**: A single slash `/` at the beginning of an XPath expression represents the root node.
    - **Example**: `/bookstore`
    - **Result**: Selects the root `<bookstore>` element.

- **Selecting All Child Nodes (`//`)**: A double slash `//` selects nodes anywhere in the document, regardless of their position in the hierarchy.
    - **Example**: `//book`
    - **Result**: Selects all `<book>` elements in the document.
        > Note that if we write the XPath as `//book/title` , then it selects all the `<title>` elements that are a direct child of the `<book>` element.

### 2. **Predicates (`[]`)**

Predicates are conditions within square brackets `[]` that filter nodes based on specified criteria.

- **Example**: `//book[@category='fiction']`
    - **Explanation**: Selects all `<book>` elements where the `category` attribute equals "fiction".
    - **Result**: `<book category="fiction" id="bk101">` and `<book category="fiction" id="bk103">`
        > If you want to get all `<book>` elements where the `category` attribute is `fiction` and `id` is `bk101`, we can use the XPath `//book[@category='fiction'][@id='bk101']`

- **Example**: `//book[price > 12]`
    - **Explanation**: Selects all `<book>` elements where the `price` element has a value greater than 12.
    - **Result**: `<book id="bk102">`, `<book id="bk104">`, and `<book id="bk103">`

### 3. **Attributes (`@`)**

In XPath, the `@` symbol is used to select attributes.

- **Example**: `//book[@id='bk102']`
    - **Explanation**: Selects the `<book>` element with an `id` attribute of "bk102".
    - **Result**: `<book category="nonfiction" id="bk102">`

- **Example**: `//title[@lang='en']`
    - **Explanation**: Selects all `<title>` elements where the `lang` attribute equals "en".
    - **Result**: `<title lang="en">The Great Gatsby</title>`, `<title lang="en">Sapiens</title>`, and `<title lang="en">The Sun and Her Flowers</title>`
        > Note that if you use XPath `//book/@id` it selects all the `id` attributes regardless of their position in the document. Similarly using XPath `//title/@lang` selects all the `lang` attributes regardless of their position inside the document.
- **Example**: `//title[@lang]`
    - **Explanation**: Selects all the `<title>` elements that has a `lang` attribute present. This is used very often in scraping!

### 4. **Functions**

XPath has several built-in functions that allow for more advanced querying.

- **text()**: Selects the text content of an element.
    - **Example**: `//title[text()='Sapiens']`
    - **Explanation**: Selects the `<title>` element with text "Sapiens".
    - **Result**: `<title lang="en">Sapiens</title>`

- **contains()**: Checks if a string contains a specific substring.
    - **Example**: `//title[contains(text(), 'The')]`
    - **Explanation**: Selects all `<title>` elements containing "The" in their text.
    - **Result**: `<title lang="en">The Great Gatsby</title>` and `<title lang="en">The Sun and Her Flowers</title>`

- **starts-with()**: Checks if a string starts with a specific substring.
    - **Example**: `//book[starts-with(@id, 'bk10')]`
    - **Explanation**: Selects all `<book>` elements with an `id` attribute that starts with "bk10".
    - **Result**: All `<book>` elements since they all start with "bk10".

### 5. **Axes**

Axes define the relationship between the current node and other nodes.

- **child**: Selects child elements of the current node.
    - **Example**: `//book/child::title`
    - **Explanation**: Selects the `<title>` elements that are direct children of `<book>` elements.

- **parent**: Selects the parent of the current node.
    - **Example**: `//title/parent::book`
    - **Explanation**: Selects the `<book>` elements that are parents of `<title>` elements.

- **ancestor**: Selects all ancestor elements (parents, grandparents, etc.) of the current node.
    - **Example**: `//price/ancestor::bookstore`
    - **Explanation**: Selects the `<bookstore>` element as it is an ancestor of `<price>` elements.

- **descendant**: Selects all descendants (children, grandchildren, etc.) of the current node.
    - **Example**: `/bookstore/descendant::title`
    - **Explanation**: Selects all `<title>` elements within `<bookstore>`.

- **following-sibling**: Selects all siblings after the current node.
    - **Example**: `//book[author='F. Scott Fitzgerald']/following-sibling::book`
    - **Explanation**: Selects all `<book>` elements that appear after the `<book>` element with author "F. Scott Fitzgerald".

### If Advanced Axes doesnt work!
If certain XPath expressions using axes like `ancestor::`, `descendant::`, `parent::`, and `following-sibling::` are not working, we can replace them with alternative XPath expressions that achieve the same result without relying on these axes. Here’s a revised list with alternative solutions.

#### Revised XPath Expressions Without Using Advanced Axes


- **child**: Selects child elements of the current node.
    - **Example**: `//book/title`
    - **Explanation**: Selects `<title>` elements that are direct children of `<book>` elements.
    - **No change needed**, as this does not rely on any special axis and should work reliably.


- **parent**: Selects the parent of the current node.
    - **Original Example**: `//title/parent::book`
    - **Revised Example**: `//book[title]`
    - **Explanation**: Selects all `<book>` elements that contain a `<title>` element. This avoids the `parent::` axis by selecting `<book>` elements based on the presence of a `<title>` child.
        > Note tha if the XPath is `//book[title = 'The Sun and Her Flowers']` , then it selects the `<book>` element that has the `<title>` element and the text inside the title is `The Sub and Her Flowers`


- **ancestor**: Selects all ancestor elements (parents, grandparents, etc.) of the current node.
    - **Original Example**: `//price/ancestor::bookstore`
    - **Revised Example**: `/bookstore[.//price]`
    - **Explanation**: Selects the `<bookstore>` element if it contains any `<price>` element, avoiding the `ancestor::` axis by checking if `<price>` exists as a descendant within `<bookstore>`.
        > Note that in the earlier example, where we deal with parent node, writing the XPath as `//book[.//title]` gives use the same result! This follows the ancestor rule that we just stated. 


- **descendant**: Selects all descendants (children, grandchildren, etc.) of the current node.
    - **Original Example**: `/bookstore/descendant::title`
    - **Revised Example**: `/bookstore//title`
    - **Explanation**: Selects all `<title>` elements within `<bookstore>`, using `//title` to find all descendant `<title>` elements under `<bookstore>`, which achieves the same result without `descendant::`.


- **following-sibling**: Selects all siblings after the current node.
    - **Original Example**: `//book[author='F. Scott Fitzgerald']/following-sibling::book`
    - **Revised Example**: `(//book[author='F. Scott Fitzgerald'])[1]/following::book`
    - **Explanation**: Selects all `<book>` elements that appear after the first `<book>` with `author="F. Scott Fitzgerald"`. Here, `following::book` will select any `<book>` nodes that appear after the specified `<book>`, not just direct siblings.


### 6. **Logical Operators**

Logical operators are used to combine multiple conditions in an XPath expression.

- **and**: Combines two conditions, both must be true.
    - **Example**: `//book[@category='fiction' and price > 10]`
    - **Explanation**: Selects `<book>` elements with category "fiction" and a price greater than 10.
    - **Result**: `<book id="bk101">` and `<book id="bk103">`

- **or**: Combines two conditions, either can be true.
    - **Example**: `//book[@category='fiction' or @category='poetry']`
    - **Explanation**: Selects all `<book>` elements with a category of "fiction" or "poetry".
    - **Result**: `<book id="bk101">`, `<book id="bk103">`, and `<book id="bk104">`

- **not()**: Negates a condition.
    - **Example**: `//book[not(@category='fiction')]`
    - **Explanation**: Selects all `<book>` elements where the `category` is not "fiction".
    - **Result**: `<book id="bk102">` and `<book id="bk104">`

### 7. **Positional Operators**

Positional operators are used to select nodes based on their position within a list.

- **[n]**: Selects the nth child (1-based index).
    - **Example**: `//book[1]`
    - **Explanation**: Selects the first `<book>` element.
    - **Result**: `<book id="bk101">`

- **last()**: Selects the last node in a list of nodes.
    - **Example**: `//book[last()]`
    - **Explanation**: Selects the last `<book>` element.
    - **Result**: `<book id="bk104">`

- **[position() < n]**: Selects nodes before the nth position.
    - **Example**: `//book[position() < 3]`
    - **Explanation**: Selects the first two `<book>` elements.
    - **Result**: `<book id="bk101">` and `<book id="bk102">`

### 8. **Wildcards**

Wildcards allow for flexible selection of nodes without specifying exact names.

- **`*`**: Matches any element node.
    - **Example**: `//book/*`
    - **Explanation**: Selects all child nodes of `<book>` elements.
    - **Result**: `<title>`, `<author>`, `<price>`, `<year>`

- **`@*`**: Matches any attribute.
    - **Example**: `//book/@*`
    - **Explanation**: Selects all attributes of `<book>` elements.
    - **Result**: `category` and `id` attributes of each `<book>`

### Summary Table of XPath Examples

| XPath Expression                      | Explanation                                                      | Result (on Example XML)                                      |
|---------------------------------------|------------------------------------------------------------------|--------------------------------------------------------------|
| `/bookstore`                          | Selects the root node                                            | `<bookstore>`                                                |
| `//book`                              | Selects all `<book>` elements                                    | All `<book>` elements                                        |
| `//book[@category='fiction']`         | Selects books with category "fiction"                            | `<book id="bk101">` and `<book id="bk103">`                  |
| `//title[@lang='en']`                 | Selects `<title>` elements where `lang="en"`                     | `<title>The Great Gatsby</title>`, etc.                      |
| `//book[price > 12]`                  | Selects books with a price greater than 12                       | `<book id="bk102">`, `<book id="bk104">`, `<book id="bk103">`|
| `//book[author='Rupi Kaur']`          | Selects books where the author is "Rupi Kaur"                    | `<book id="bk104">`                                          |
| `//book/title/text()`                 | Selects text of all `<title>` elements                           | "The Great Gatsby", "Sapiens", etc.                          |
| `//book[position()=1]`                | Selects the first `<book>` element                               | `<book id="bk101">`                                          |
| `//book[last()]`                      | Selects the last `<book>` element                                | `<book id="bk104">`                                          |
| `//book/*`                            | Selects all child elements of each `<book>`                      | All child elements of each `<book>`                          |

These XPath expressions cover the essential components, making XPath a powerful tool for navigating and querying XML documents.

---