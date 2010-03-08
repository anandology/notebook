# jsdef - templetor extensions to support javascript templating

jsdef extension adds a new block `jsdef` to [templetor][1] syntax. The `jsdef` block defines a template function and also generates an equivalent JavaScript function.

[1]: http://webpy.org/docs/0.3/templetor

This extension works only with the development branch of web.py.

<http://github.com/webpy/webpy>

## How to use

Tell web.py to use the extension.

    import web
    import jsdef
    
    render = web.template.render("templates", extensions=[jsdef.extension])
    
Include [jsdef.js](jsdef.js) in your site template.

And use `jsdef` in your templates.

    $def with (page)
    
    <h1>$page.title</h1>
    
    $jsdef render_books(books):
        <ul>
            $for book in books:
                <li><a href="$book.key">$book.title</a></li>
        </ul>
                
    <div class="books">
        $# Above jsdef block has defined render_books template function. Use it when rendering the template.
        $:render_books(page.books)
    </div>
        
    <script type="test/javascript">
        function update_books(books) {
            // Above jsdef block has generated javascript for render_books function. Use it at the client.
            document.getElementById("books").innerHTML = render_books(books);
        }
    </script>
    
## Caveats
This is just an attempt to drive JavaScript templating from Python. Features like multiple assignments, list slicing, list comprehensions won't work. 

If you are using a python function inside the jsdef block, you need to provide the equivalent in JavaScript too. Some builtin functions are already provided by [jsdef.js](jsdef.js).

