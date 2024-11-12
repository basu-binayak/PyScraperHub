# Web Scraping

<img src="./images/web-scraping.png">

**Web scraping** is the automated process of extracting data from websites. This data extraction is typically done by a **web scraper**, which is a program or script designed to navigate websites, locate specific pieces of information, and save them in a structured format (such as CSV, JSON, or databases) for analysis, reporting, or other uses.

## How Web Scraping Works?

Web scraping usually involves the following steps:
1. **Sending HTTP Requests**: The web scraper sends a request (typically HTTP GET) to the target website’s server to access a web page.
    > Hypertext Transfer Protocol (HTTP) is an application protocol that transfers resources (web-based), such as HTML documents, between a client and a web server. HTTP is a stateless protocol that follows the client-server model. Clients (web browsers) and web servers communicate or exchange information using HTTP requests and HTTP responses.
2. **Parsing the HTML**: Once the server responds with the HTML of the page, the scraper parses the HTML to locate specific elements.
3. **Locating and Extracting Data**: Using HTML tags, attributes, and classes (like `<div>`, `<span>`, `class="title"`, etc.), the scraper pinpoints and extracts the relevant data.
4. **Storing the Data**: The extracted data is then organized and stored in a structured format, such as CSV, JSON, or a database.

## Example Use Cases for Web Scraping
- **Price Comparison**: Aggregating product prices from different e-commerce sites.
- **Market Research**: Collecting data on competitors, customer reviews, or trends.
- **Content Aggregation**: Gathering news, articles, or blog posts from multiple sources.
- **Job Listings**: Scraping job listings from various job boards for data analysis.
- **Real Estate Listings**: Extracting property data for analysis or listing on another platform.

## Tools and Libraries for Web Scraping
There are various tools and libraries designed for web scraping, depending on the level of control and the programming language you prefer:
- **Python Libraries**: BeautifulSoup, Scrapy, Selenium (for JavaScript-heavy sites).
- **Dedicated Tools**: Octoparse, ParseHub, or web scraping APIs like ScraperAPI.

## Ethical and Legal Considerations
Web scraping has legal and ethical implications, as some websites have terms of service prohibiting automated access. It's important to:
- **Respect Robots.txt**: Check the website's `robots.txt` file to see what pages allow or disallow scraping.
- **Avoid Overloading Servers**: Set reasonable delays between requests to prevent overwhelming the server.
- **Abide by Terms of Service**: Ensure that your scraping practices comply with the website’s terms of service and applicable laws.

In summary, web scraping is a powerful tool for gathering data automatically from websites. However, it should be done responsibly and ethically to ensure respect for site owners and users.

# Introducing XPath and CSS Selectors to process markup documents

## HTML (HyperText Markup Language) and XML (eXtensible Markup Language) Markup Documents

**HTML** and **XML** are both markup languages used to structure and format data. While they share some similarities in syntax, they are designed with different purposes and use cases in mind.

---

### HTML: HyperText Markup Language

**Purpose**: HTML is the standard markup language used for creating and designing web pages and web applications.

**Key Characteristics**:
- **Fixed Tags**: HTML has a predefined set of tags (like `<div>`, `<p>`, `<a>`, etc.) used to structure content on the web. These tags have specific meanings and are limited in scope.
- **Presentation and Structure**: HTML is focused on the **presentation** of information, meaning that tags define how content is displayed on the web (e.g., `<h1>` for headers, `<p>` for paragraphs).
- **Flexible Syntax**: HTML is more lenient with syntax errors. Web browsers can often handle improperly nested tags and missing closing tags.
- **Attributes**: HTML elements can contain attributes that modify their appearance or behavior, such as `id`, `class`, and `style`.
  
**Example of HTML**:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Sample HTML Document</title>
</head>
<body>
    <h1>Welcome to My Website</h1>
    <p>This is a sample paragraph.</p>
</body>
</html>
```

### XML: eXtensible Markup Language

**Purpose**: XML is a flexible markup language used primarily for **storing** and **transporting** data in a structured format.

**Key Characteristics**:
- **Customizable Tags**: XML allows users to define their own tags, which makes it suitable for data exchange between systems. There are no predefined tags, and XML is entirely customizable.
- **Data Focused**: Unlike HTML, XML is **data-centric**. It does not focus on displaying data but rather on representing it in a way that can be easily understood and transferred across different applications.
- **Strict Syntax**: XML requires strict syntax; every opening tag must have a corresponding closing tag, and tags must be properly nested. This rigidity ensures data consistency.
- **Attributes and Nesting**: XML elements can contain attributes and can be nested to create a hierarchical structure, making it ideal for complex data representation.

**Example of XML**:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
    <book>
        <title>Sample Book Title</title>
        <author>John Doe</author>
        <price currency="USD">29.99</price>
    </book>
</bookstore>
```


### Key Differences Between HTML and XML

| Feature                  | HTML                                                       | XML                                                            |
|--------------------------|------------------------------------------------------------|----------------------------------------------------------------|
| **Purpose**              | Web content and page structure                             | Data storage and transfer                                      |
| **Tag Set**              | Predefined, fixed set of tags                              | Customizable, user-defined tags                                |
| **Syntax Flexibility**   | Flexible, forgiving of minor syntax errors                 | Strict syntax, requires well-formed documents                  |
| **Data Focus**           | Focuses on presentation and display of data                | Focuses on the structure and portability of data               |
| **Usage of Attributes**  | Commonly used to add style and behavior (`id`, `class`)    | Used to store additional data but not commonly for presentation|
| **Data vs. Presentation**| Presentation-oriented                                      | Data-oriented                                                  |


### Use Cases

- **HTML**: Designing web pages, web applications, email templates, and other content to be viewed in browsers.
- **XML**: Data interchange between systems (e.g., REST APIs, SOAP messages), configuration files, document formats (e.g., RSS feeds, SVG files).

In summary, HTML is ideal for content and presentation on the web, while XML is ideal for defining and structuring data for storage and exchange. Both markup languages are essential in web development, though they serve distinct purposes.

## Document Object Model (DOM)

The **Document Object Model (DOM)** is a programming interface for web documents, representing the structure, style, and content of a document in a **tree-like structure**. It allows developers to access, manipulate, and modify the content and structure of HTML and XML documents dynamically. The DOM is a key concept in web development, as it enables interactive and dynamic websites by letting developers update content, style, and behavior of web pages on the fly.

### Key Points About the DOM:
1. **Tree Structure**: The DOM represents the document as a hierarchical tree of nodes, where each node corresponds to a part of the document, such as an HTML element, attribute, or text.
2. **Programming Interface**: Using languages like JavaScript, developers can interact with the DOM to change or retrieve information from the document.
3. **Dynamic and Live**: The DOM is a live representation, meaning that any change made to the DOM is immediately reflected in the visible web page.

### Structure of the DOM

In the DOM tree structure:
- **Document**: The top node represents the entire HTML or XML document.
- **Element Nodes**: Each HTML tag (like `<div>`, `<h1>`, `<p>`, etc.) becomes an element node.
- **Text Nodes**: The actual text within an element is represented as a text node.
- **Attribute Nodes**: Each HTML attribute (like `id`, `class`, `href`, etc.) is represented as an attribute node.

For example, consider the following HTML document:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Sample Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is a sample paragraph.</p>
</body>
</html>
```

The DOM tree for this HTML would look like this:

```
Document
└── html
    ├── head
    │   └── title ("Sample Page")
    └── body
        ├── h1 ("Hello, World!")
        └── p ("This is a sample paragraph.")
```

The DOM is a foundational technology in web development that enables a wide range of functionalities on websites. Through DOM manipulation, developers can create responsive and dynamic web applications that can adjust in real time to user interactions and data updates, providing a more engaging experience for users.

## XPath in detail

Let’s walk through **XPath** in detail with an example XML document. XPath (XML Path Language) is a query language for selecting and navigating nodes in an XML document. It is used widely to extract specific data from XML documents based on a structured path.

### Example XML Document

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

---

### XPath Syntax and Components

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
    - **Example**: `/bookstore/book/child::title`
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



---

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