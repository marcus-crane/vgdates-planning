# What is VGDates meant to be?

I often wonder what games are coming up and it can be an annoying process!

Specifically, I wish I had a site that is

- Single serving
  - In the case of game journalism sites, release dates usually take the form of a wiki or a blog post which wasn't is most efficient layout.
  - More "traditional" sites like Metacritic can take a lot of clicking to get the information I want. They primarily serve other functions and keeping upcoming titles updated isn't their focus.
- Easy to parse both visually and technically
  - There's a number of lists that may be hugely comprehensive, like Giant Bomb, but there's almost too much excess data like ratings or resolution. It's hard to just glimpse at the information and be done.
  - While Giant Bomb has an API, other sites just serve up plain HTML which can be a pain in the ass if you want to (and are allowed to) repurpose it.
- Up to date
  - Giant Bomb is great but being user sourced, it can be missing information.
  - Wiki/blog post sites can take a long time to get updated with new titles and take a bit to prune older titles as well.
  -Publishers may push back dates or outright cancel games leading to confusion as to what dates are correct!

I've started and stopped this project a few times mainly messing around changing up how I would approach it.

I think my final answer will likely be a standalone API that allows some rough sorting and a seperate client side application that displays it all. That way, if anyone else wants to use the data in a different format or for personal use, they can go on ahead.

I haven't given any thought to API keys or anything like that. That's what this planning repo is for!