
**From request to response - How does the Web Works**

The web is everywhere!

We use it more than we ever did before - also in many places where you might not see it. Because "the web" is more than just websites you visit by entering a URL in your browser.

No matter if you check your emails on your mobile phone or if you're sending a tweet - you are using the internet (i.e. "the web").

**a.  Main functionality of the browser**

The main function of a browser is to present the web resource you choose, by requesting it from the server and displaying it in the browser window. The resource is usually an HTML document, but may also be a PDF, image, or some other type of content. The location of the resource is specified by the user using a URI (Uniform Resource Identifier).

The way the browser interprets and displays HTML files is specified in the HTML and CSS specifications. These specifications are maintained by the W3C (World Wide Web Consortium) organization, which is the standards organization for the web. For years browsers conformed to only a part of the specifications and developed their own extensions. That caused serious compatibility issues for web authors. Today most of the browsers more or less conform to the specifications.

Browser user interfaces have a lot in common with each other. Among the common user interface elements are:

-   Address bar for inserting a URI
    
-   Back and forward buttons
    
-   Bookmarking options
    
-   Refresh and stop buttons for refreshing or stopping the loading of current documents
    
-   Home button that takes you to your home page
    

  

![](https://lh3.googleusercontent.com/OrQOheyaIBR0lGZDXdHjKp0VizU_2IwLxciINs6kf2u1QQYTWIUyyimtrzYX26ISg2tYyPcEJ6OZ-ZceL4yq3L6xKSW6Kx9EJbIMqsYp8vfbUE8Si2MMtDX-42qNKdyz6NHT-R29hwSJRZYSCg)

**b. High Level Components of a browser**
    
-   The user interface: this includes the address bar, back/forward button, bookmarking menu, etc. Every part of the browser displays except the window where you see the requested page.
    
-   The browser engine: marshals actions between the UI and the rendering engine.
    
-   The rendering engine: responsible for displaying requested content. For example if the requested content is HTML, the rendering engine parses HTML and CSS, and displays the parsed content on the screen.
    
-   Networking: for network calls such as HTTP requests, using different implementations for different platforms behind a platform-independent interface.
    
-   UI backend: used for drawing basic widgets like combo boxes and windows. This backend exposes a generic interface that is not platform specific. Underneath it uses operating system user interface methods.
    
-   JavaScript interpreter: Used to parse and execute JavaScript code.
    
-   Data storage: This is a persistence layer. The browser may need to save all sorts of data locally, such as cookies. Browsers also support storage mechanisms such as localStorage, IndexedDB, WebSQL and FileSystem.
    

  

**c. Rendering Engine**
    

By default the rendering engine can display HTML and XML documents and images. It can display other types of data via plug-ins or extensions; for example, displaying PDF documents using a PDF viewer plug-in.

  

The rendering engine will start getting the contents of the requested document from the networking layer. This will usually be done in 8kB chunks. After that, this is the basic flow of the rendering engine:

![](https://lh5.googleusercontent.com/2FZwIBi0xQe6oQJ6o_JZkRsjET-7PtYgVtnJS0ci0-7EDWdoFESPu_eVqEzwISrZk_Gv8iPbfWEEWU98GwQGFoddsU8qbnv4zHyIacJZkhKN1WXLc9LkO60iCzsnyfLeOg_nT25SiCeRhsM8nQ)

The rendering engine will start parsing the HTML document and convert elements to DOM nodes in a tree called the "content tree". The engine will parse the style data, both in external CSS files and in style elements. Styling information together with visual instructions in the HTML will be used to create another tree: the render tree.

  

The render tree contains rectangles with visual attributes like color and dimensions. The rectangles are in the right order to be displayed on the screen.

  

After the construction of the render tree it goes through a "layout" process. This means giving each node the exact coordinates where it should appear on the screen. The next stage is painting - the render tree will be traversed and each node will be painted using the UI backend layer.

  

It's important to understand that this is a gradual process. For better user experience, the rendering engine will try to display contents on the screen as soon as possible. It will not wait until all HTML is parsed before starting to build and layout the render tree. Parts of the content will be parsed and displayed, while the process continues with the rest of the content that keeps coming from the network.

  

![](https://lh3.googleusercontent.com/S7S664CsecPe6lt8cCwx7w82v5J7g6agDs5zhsA0_A69IDnIWZZ-LiaLjy8nGyQFQ_QfhARj6e5V-VtvxRFV_JsLbtOTmBSHcwkMRhdgwkqsySbzq-tRbT376oNTN7hlzP3H2gIkT_q3NZ9WkQ)

  

To parse HTML documents, and more generally XML, the rendering engine uses the XML parser. Mozilla’s JavaScript engine, SpiderMonkey, executes JavaScript on Web pages. The networking subsystem, Necko, handles all network traffic in the browser. The rendering engine and user interface use a display backend for drawing. The graphic libraries provide primitives for drawing and windowing, user interface, widgets, and fonts. Data persistence in Firefox is provided by Mozilla’s profile mechanism. This data store contains all data such as bookmarks, cookies, and page caches.

  

**d.  Parsers**
    

  

Parsing a document means translating it to a structure the code can use. The result of parsing is usually a tree of nodes that represent the structure of the document. This is called a parse tree or a syntax tree.

  

For example, parsing the expression 2 + 3 - 1 could return this tree:

![](https://lh4.googleusercontent.com/G4ZIcb8bNEaqpzNuXj9dmdqgV8s71PV30r3btY-Hn2Y19p7WvLcNNCXnJstTR5KravcGs6KzhuuLmhBpd1wIxJw9vouF1D3Tbiigkf8q691k23Kv4ahOQjAMEmH39cpR-EpryQT7mCbFTbufpg)

  

Parsing is based on the syntax rules the document obeys: the language or format it was written in. Every format you can parse must have deterministic grammar consisting of vocabulary and syntax rules. It is called context free grammar. Human languages are not such languages and therefore cannot be parsed with conventional parsing techniques.

  

**Parser - Lexer combination**

  

Parsing can be separated into two sub processes: lexical analysis and syntax analysis.

  

Lexical analysis is the process of breaking the input into tokens. Tokens are the language vocabulary: the collection of valid building blocks. In human language it will consist of all the words that appear in the dictionary for that language.

  

Syntax analysis is the application of the language syntax rules.

  

Parsers usually divide the work between two components: the lexer (sometimes called tokenizer) that is responsible for breaking the input into valid tokens, and the parser that is responsible for constructing the parse tree by analyzing the document structure according to the language syntax rules.

  

The lexer knows how to strip irrelevant characters like white spaces and line breaks.

  

![](https://lh4.googleusercontent.com/p9xAHaRGOfifCuV4qb7YLY2_l25gvU25eWpz0wF7H6YtHWePBtrdTkSU7MVi4Fvy9LYyef11vkf1MoVYAvhx4SeCjORBkD81YKkRNxM8zUnzzzqXScpYfIiSeuv8EGTjjyrz3gTJbduO6MffgA)

  

The parsing process is iterative. The parser will usually ask the lexer for a new token and try to match the token with one of the syntax rules. If a rule is matched, a node corresponding to the token will be added to the parse tree and the parser will ask for another token.

  

If no rule matches, the parser will store the token internally, and keep asking for tokens until a rule matching all the internally stored tokens is found. If no rule is found then the parser will raise an exception. This means the document was not valid and contained syntax errors.

  

**HTML Parser**

  

The job of the HTML parser is to parse the HTML markup into a parse tree.

  

**The HTML grammar definition**

  

The vocabulary and syntax of HTML are defined in specifications created by the W3C organization.

  

**Not a context free grammar**

  

There is a formal format for defining HTML - DTD (Document Type Definition) - but it is not a context free grammar.

On one hand this is the main reason why HTML is so popular: it forgives your mistakes and makes life easy for the web author. On the other hand, it makes it difficult to write formal grammar. So to summarize, HTML cannot be parsed easily by conventional parsers, since its grammar is not context free. HTML cannot be parsed by XML parsers.

  

**HTML DTD**

  

HTML definition is in a DTD format. This format is used to define languages of the SGML family. The format contains definitions for all allowed elements, their attributes and hierarchy.

  

There are a few variations of the DTD. The strict mode conforms solely to the specifications but other modes contain support for markup used by browsers in the past. The purpose is backwards compatibility with older content.

  

**DOM**

  

The output tree (the "parse tree") is a tree of DOM elements and attribute nodes. DOM is short for Document Object Model. It is the object presentation of the HTML document and the interface of HTML elements to the outside world like JavaScript.

  

The root of the tree is the "Document" object.

  

This markup would be translated to the following DOM tree:

  

![](https://lh4.googleusercontent.com/xOvC-FkXtfrrhj3v1L6GXYHDjcDm2rOYAJ4MUQsLmzERLMwWnGSHLw-DBC5foTXwHQA0UjiB0pVRGwoBZgrGD6X8NZLqyYAYLiWPYvV4dGoV2JV0LhtWzX-K9JE-bJjwsoEEAaA5rcjJi7LK0A)

  

When I say the tree contains DOM nodes, I mean the tree is constructed of elements that implement one of the DOM interfaces. Browsers use concrete implementations that have other attributes used by the browser internally.

  

**The parsing algorithm**

  

HTML cannot be parsed using the regular top down or bottom up parsers.

  

The reasons are:

-   The forgiving nature of the language.
    
-   The fact that browsers have traditional error tolerance to support well known cases of invalid HTML.
    
-   The parsing process is reentrant. For other languages, the source doesn't change during parsing, but in HTML, dynamic code (such as script elements containing document.write() calls) can add extra tokens, so the parsing process actually modifies the input.
    

  

The algorithm consists of two stages: tokenization and tree construction.

  

Tokenization is the lexical analysis, parsing the input into tokens. Among HTML tokens are start tags, end tags, attribute names and attribute values.

  

The tokenizer recognizes the token, gives it to the tree constructor, and consumes the next character for recognizing the next token, and so on until the end of the input.

  

![](https://lh3.googleusercontent.com/td30LfPIJgDAcfKnDJuUN7n5Dndi0Haj55FqoYeW-jO94BZ9YKl2LrKjbQtyjYzKLut7laMbYbxU3YuY6pwAZhA7b8UxA1OB4GiLZDE2Zm8yQIbfmGoVFESBzlafuF-WXIcB79vdPDHYFuV3uw)

  

**The tokenization algorithm**

  

The algorithm's output is an HTML token. The algorithm is expressed as a state machine. Each state consumes one or more characters of the input stream and updates the next state according to those characters. The decision is influenced by the current tokenization state and by the tree construction state. This means the same consumed character will yield different results for the correct next state, depending on the current state.

  

![](https://lh6.googleusercontent.com/oUfSN7-nN1wp3eLd6FDG1xUstiSmhgc6lmdlRJACgC_JMm72D0_2tKUfGy2FyHUI6ICFPS7Bni-p_jm-2NwpKmiPaOmU0cR2f7sx82L-VcFgRkaTaoybHPc3hMrklEXyrIj0EInra7BAwz5xcg)

  

**Tree construction algorithm**

  

When the parser is created the Document object is created. During the tree construction stage the DOM tree with the Document in its root will be modified and elements will be added to it. Each node emitted by the tokenizer will be processed by the tree constructor. For each token the specification defines which DOM element is relevant to it and will be created for this token. The element is added to the DOM tree, and also the stack of open elements. This stack is used to correct nesting mismatches and unclosed tags. The algorithm is also described as a state machine. The states are called "insertion modes".

  

![](https://lh3.googleusercontent.com/TkiRk7sv_YP7tXMP2kJYSzvsVC7ALqeXrVJvhBrtMIxUAx5khcaBxZG9LsX-WyDqcJcsPzAZndvbF5fKz1mjRayBuTn2t0sTRZlzOfjg7T5TM64Sd-ZVyB7_oHlTenVmORlo-xyRn-BJKDvO3w)

  

**Actions when the parsing is finished**

  

At this stage the browser will mark the document as interactive and start parsing scripts that are in "deferred" mode: those that should be executed after the document is parsed. The document state will be then set to "complete" and a "load" event will be fired.

  

**Browsers' error tolerance**

  

We have to take care of at least the following error conditions:

-   The element being added is explicitly forbidden inside some outer tag. In this case we should close all tags up to the one which forbids the element, and add it afterwards.
    
-   We are not allowed to add the element directly. It could be that the person writing the document forgot some tag in between (or that the tag in between is optional). This could be the case with the following tags: HTML HEAD BODY TBODY TR TD LI (did I forget any?).
    
-   We want to add a block element inside an inline element. Close all inline elements up to the next higher block element.
    
-   If this doesn't help, close elements until we are allowed to add the element - or ignore the tag.
    

  

**CSS parsing**

  

WebKit uses Flex and Bison parser generators to create parsers automatically from the CSS grammar files. As you recall from the parser introduction, Bison creates a bottom up shift-reduce parser. Firefox uses a top down parser written manually. In both cases each CSS file is parsed into a StyleSheet object. Each object contains CSS rules. The CSS rule objects contain selector and declaration objects and other objects corresponding to CSS grammar.

  

![](https://lh6.googleusercontent.com/hIxSPC7-q3IQnfHJ2MWT_XWy99QC9Ol1zLRI68alGoGlKZWeBsF8pWqoNd8qUWgEG-Ip0AzmaaIIIYO0tVJVB7mZGRZR2QBTYHPxdVdEvpCz8oJHmNe1P5Rba3SapkTLjGYAYuF_-rO-xqPmUg)

  

**e.  Script Processors and The order of processing scripts**
    

  

**Scripts**

  

The model of the web is synchronous. Authors expect scripts to be parsed and executed immediately when the parser reaches a <script> tag. The parsing of the document halts until the script has been executed. If the script is external then the resource must first be fetched from the network - this is also done synchronously, and parsing halts until the resource is fetched. This was the model for many years and is also specified in HTML4 and 5 specifications. Authors can add the "defer" attribute to a script, in which case it will not halt document parsing and will execute after the document is parsed. HTML5 adds an option to mark the script as asynchronous so it will be parsed and executed by a different thread.

  

**Speculative parsing**

  

Both WebKit and Firefox do this optimization. While executing scripts, another thread parses the rest of the document and finds out what other resources need to be loaded from the network and loads them. In this way, resources can be loaded on parallel connections and overall speed is improved. Note: the speculative parser only parses references to external resources like external scripts, style sheets and images: it doesn't modify the DOM tree - that is left to the main parser.

  

**f.  Tree Construction**
    

  

While the DOM tree is being constructed, the browser constructs another tree, the render tree. This tree is of visual elements in the order in which they will be displayed. It is the visual representation of the document. The purpose of this tree is to enable painting the contents in their correct order.

  

Firefox calls the elements in the render tree "frames". WebKit uses the term renderer or render object.

  

A renderer knows how to lay out and paint itself and its children.

  

**The render tree relation to the DOM tree**

  

![](https://lh5.googleusercontent.com/M6kCmBsBE6GLVgHzfdurcIpJyZXCdmjs4On7-UbYSSpjvqoVxPFlGO6Izj8aGUpUurLRn23WnN417NRg3WxLD4rY7Zoxt0OWYGGNSkl-HrcfsW00TaNZXups5EXsbKamPV-IKf827rV384QEVA)

  

**h. Layout and Printing**

  

**Layout:** When the renderer is created and added to the tree, it does not have a position and size. Calculating these values is called layout or reflow.

  

HTML uses a flow based layout model, meaning that most of the time it is possible to compute the geometry in a single pass. Elements later "in the flow" typically do not affect the geometry of elements that are earlier "in the flow", so layout can proceed left-to-right, top-to-bottom through the document. There are exceptions: for example, HTML tables may require more than one pass.

  

The coordinate system is relative to the root frame. Top and left coordinates are used.

  

Layout is a recursive process. It begins at the root renderer, which corresponds to the <html> element of the HTML document. Layout continues recursively through some or all of the frame hierarchy, computing geometric information for each renderer that requires it.

  

The position of the root renderer is 0,0 and its dimensions are the viewport - the visible part of the browser window.

  

All renderers have a "layout" or "reflow" method, each renderer invokes the layout method of its children that need layout.

  

**Painting:** In the painting stage, the render tree is traversed and the renderer's "paint()" method is called to display content on the screen. Painting uses the UI infrastructure component.
