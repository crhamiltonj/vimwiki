# Semantic HTML

See this article for reasoning behind sectioning elements
[How to use the HTML5 Sectioning Elements](https://blog.teamtreehouse.com/use-html5-sectioning-elements)

and this article for what to use when
[HTML5 Semantic Tags](http://www.vikingcodeschool.com/html5-and-css3/html5-semantic-tags)

- header -- Header content such as logo and searchbox
- nav -- Navigation entries such as a main or feature menu
- main -- The main content of the page
- section -- seprates different sections
- article -- any type of repeatable content
- aside -- content not directly related to the main section
- footer -- Content such as copyright, ptivacy and TOS, contact info etc.

## Boilerplate Semantic HTML Markup

```text
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Landing Page</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <header>

    </header>
    <nav>

    </nav>
    <main>
        <section>
            <article></article>
        </section>
    </main>
    <aside>
    </aside>
    <footer>
    </footer>
  </body>
</html>
```