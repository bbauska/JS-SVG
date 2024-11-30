# JS-SVG
## JavaScript and SVG Generative Art with JavaScript and SVG
### Utilizing Scalable Vector Graphics and Algorithms for Creative Coding and Design

Design Thinking is a set of strategic and creative processes and principles
used in the planning and creation of products and solutions to human-
centered design problems.
With design and innovation being two key driving principles, this
series focuses on, but is not limited to, the following areas and topics:

  - User Interface (UI) and User Experience (UX) Design
  - Psychology of Design
  - Human-Computer Interaction (HCI)
  - Ergonomic Design
  - Product Development and Management
  - Virtual and Mixed Reality (VR/XR)
  - User-Centered Built Environments and Smart Homes
  - Accessibility, Sustainability and Environmental Design
  - Learning and Instructional Design
  - Strategy and best practices

This series publishes books aimed at designers, developers, storytellers
and problem-solvers in industry to help them understand current
developments and best practices at the cutting edge of creativity, to invent
new paradigms and solutions, and challenge Creatives to push boundaries
to design bigger and better than before.

# Generative Art with JavaScript and SVG Utilizing Scalable Vector Graphics and Algorithms for Creative Coding and Design

## Introduction
### What You Should Know
As a reader, what should you know before tackling this book? It will
no doubt be easier if you are comfortable with the core concepts of
programming, like variables, functions, loops, and conditionals. These
kinds of concepts carry over from language to language, differing mainly
with respect to syntax, so if you come from a language other than
JavaScript, then that’s completely fine.
If you have no prior programming experience, we will be covering
the concepts required in Chapter 2, but I should emphasize that this
book is not intended to be an introduction to programming. The second
chapter is best thought of as a primer, a jumping-off point for a deeper
dive elsewhere. A short introductory course would really benefit you here.
Personally I’d recommend the wonderful freeCodeCamp.com, a site I’ve
spent many hours using myself. It offers free interactive tutorials on the
basics of HTML, CSS, and JavaScript, and much more besides.
For those coming from another language, like Python, PHP, or C#, the
second chapter may still be valuable, to be sure you’re acquainted with the
syntax and some of the idiosyncrasies of JavaScript.
If you’re already a practicing web developer, you could skip (or
quickly skim) Chapter 2, depending on your level of experience. If you’re
unfamiliar with any of the techniques or syntax used in our opening
example (which we’ll end Chapter 1 with), I’d encourage you to give the
second chapter a read, where they’ll be fully explained. The field of web
development is vast enough that what is bread and butter to one developer
might be bleeding edge to another.

### Tools
On the tool end of things, we’ll be using the following:
  - JavaScript and the SvJs library. I’ll elaborate on this further later.
  - A code editor. Here I’ll be giving you a choice between
    - Visual Studio Code (an excellent open source code editor)
    - CodePen (a popular online code editor)
  - If you opt to use Visual Studio Code (which I recommend), we’ll also be using Node.js and NPM to manage dependencies (a good habit to get into as a developer).

All code examples are available on both GitHub and CodePen, so feel
free to follow along whichever way you prefer. You can of course do both,
work locally with a code editor but check out CodePen examples online for
quick inspiration. For convenience, I’ll organize and embed all CodePen
examples at davidmatthew.ie/generative-art-javascript-svg.

### Techniques
In terms of the techniques we’ll tackle, by the end of this book, you should
have a good overview of the following:
  - The main functionality of the SvJs library and how it relates to the SVG spec
  - Creating generative art sketches with JavaScript using ES6+ syntax
  - Generating primitive SVG shapes
  - Creating iterative variations of sketches by randomizing parameters
  - Using noise to create organic variance
  - Generating complex SVG paths
  - Making sketches interactive
  - Animating sketches
  - Using SVG filters generatively

We’ll be covering a lot of ground, so don’t put yourself under pressure
to understand everything. I must have encountered certain programming
concepts umpteen times before the proverbial penny finally dropped
(JavaScript promises anyone?), and whenever understanding did finally
dawn, it would usually be because I was experimenting with something I
wanted to build, rather than repeating tutorial steps by rote. Tutorials and
instructional books certainly have their place (I wouldn’t be writing this
book otherwise), but it’s important that you take what you want from them,
rather than seeing them as syllabi to be strictly followed.
A sense of play is important, particularly when it comes to art. And
although I mentioned tools previously, I would prefer if you viewed this
book as more of a toybox than a toolbox. When I think of tools, I think of
problems that need fixing, like the loose hinges on that crooked cabinet
you’re going to tighten any day now. Tools tend to be more functional than
fun, and I’d like you to have some fun with this book.

## The Beginner’s Path
Before journeying along any path, the groundwork needs to be in place.
In this opening chapter, that’s what we’ll do, lay the groundwork. We’ll
introduce SVG, explain what makes it a uniquely powerful image format,
and show how it can be used with JavaScript to create generative art. In the
process, we’ll set up our tools and a template we can use for subsequent
sketches.

### Why JavaScript and SvJs?
Most books about generative art use a Java-based language called
Processing, or its JavaScript port p5.js. Processing was created specifically
for artists and designers new to coding and has a large and active
community. So why doesn’t this book use it?
My first forays into generative art were with Processing, so I certainly
acknowledge its value. I quickly moved to p5.js when the library was first
released in 2013, which allowed generative sketches to be written directly
in JavaScript, the language of the Web. But when I wanted to integrate
some of my own sketches into real-world web development projects, its
limitations quickly showed. It’s a large library, clocking in at close to a
megabyte at last check, and while that may not sound like much, it’s a lot
by web development standards.

The p5.js library is built on top of the HTML Canvas API, which I soon
discovered is actually quite straightforward to use. Using this API directly, I
was able to achieve much the same results as with p5.js, so that became my
go-to. However, the output of all my sketches – p5.js or Canvas – was still
resolution-dependent bitmap graphics, devoid of any semantic content.
What does that mean, and why does it matter (to me at least)? Let me
explain.

### Introducing Scalable Vector Graphics
Back in the early days of the Web, when dial-up modems were dominant
and connecting to the Internet was anything but instant, bandwidth came
at a premium. File sizes had to be super small if you wanted a page to load
in your lifetime, and bitmap images, such as JPGs and PNGs, were the
main bandwidth bottleneck.
Bitmap images – also known as raster images – are comprised of
large chunks of data (or bits), and generally speaking, if you want a larger
image, you need more bits, which means a bigger file size. SVG, on the
other hand, is a vector format, which is fundamentally different. SVG can
be scaled to any dimension, all without a corresponding increase in file
size, and it is always dazzlingly sharp and crisp. This is possible because
it doesn’t bother itself with the bits (i.e., pixels) needed to paint the image
to the screen, but rather describes the image to be rendered at a more
abstract, semantic level. And it does this in much the same way that
HTML describes the structure and content of a web page. As the Mozilla
Developer Network puts it
<blockquote>
SVG is, essentially, to graphics what HTML is to text.
</blockquote>

The SVG format was not only a powerful solution to a practical
bandwidth problem; it was a nonproprietary format officially standardized
by the World Wide Web Consortium (which is as good as future-proofing
gets in the world of web technology). The stage was set for its adoption
as far back as 1999, but unfortunately browser vendors dragged their feet
and were extremely slow to introduce support. So for the longest time (in
Internet terms at least), SVG languished in obscurity. It only really got
the support it deserved with the decline of Flash (Adobe’s proprietary
format that required a plug-in to run and was often riddled with security
vulnerabilities) and the rise of responsive design and retina (or high PPI)
screens, where its scalability and sharpness really shine.
These days we can use the format freely without worry, but to use it for
the odd icon and logo is one thing; to tap its full potential is another.

## Native SVG
As SVG is a declarative language like HTML, it’s very human-readable
and easy to get started with. Just like HTML elements, SVG elements are
written using opening and closing angle brackets and contain attributes
with values. Here, for example, is how you’d create a circle:
<circle r="125" cy="250" cx="250" fill="cyan"/>
The attributes r, cx, cy, and fill in the preceding example refer to the
circle’s radius, the x and y coordinates of its center, and the color to fill it
with. All are sensibly named and simple to follow.
Some SVG elements will contain other elements nested within them,
referred to as their child nodes or children, and will therefore need
opening and closing tags. One prominent example is the parent <svg>
element itself, which contains all other SVG elements.
As an example of how you might handwrite an SVG, here is the markup
underlying a very simple composition in the style of Hilma af Klint,
arguably the first abstract artist in Western art history.

<svg width="500" height="500" style="background-color:
#ad3622">
<title>A simple Hilma af Klint-inspired knock-off</title>
  <circle r="125" cy="250" cx="250" fill="#d0d1c9"/>
  <circle r="100" cy="250" cx="250" fill="#1c1c1c"/>
  <circle r="75" cy="250" cx="250" fill="#5085b4"/>
  <circle r="50" cy="250" cx="250" fill="#d6a946"/>
</svg>

  As you can see, SVG is written in such a way as to preserve the
semantics of the code. Search engines love this; no longer are they looking
at an impenetrable wall of pixels; they can clearly see the intent within the
markup. In this case, four circles displayed in the order they’re written,
with a title for extra accessibility. Figure 1-1 shows how this markup
appears when rendered.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  JS-SVG in js-svg.bausk.github.io ~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~ 01/02.  (01) ~~~~~~~~~~~~~~~~~~~-->
<img class="border"
  src="./images/webp/image001.webp"
  style="width:20%; float: left; margin-left: 30%; margin-bottom: 1em;"
  title="JavaScript SVG"
  alt="JavaScript SVG." />
<img class="border"
  src="./images/webp/image002.webp"
  style="width:20%; float: left; margin-left: 5%; margin-bottom: 1em;"
  title=""
  alt="." />
<p style="clear: both;"></p>
Figure 1-1. A simple composition in the style of Hilma af Klint’s Svanen (The Swan)

Declarative formats are straightforward to read, but their weakness
is that they can become tedious to write. What if we wanted 100 circles
instead of four? With native SVG, we’d have to handwrite all of them, one
after the other. And if we wanted to display our circles at random cx and
cy positions, each with a randomly selected fill, this isn’t possible at all.
Variables, loops, functions, and all the fun stuff of imperative programming
aren’t available to us. Declarative formats are concerned more with the
what of a program rather than the how. The how, however, will very
much matter to us. Without the how, we wouldn’t have algorithms, and
algorithms are essential to generative art.
Algorithms are like recipes; they contain the steps you need to follow
to achieve a certain result. If you’re baking a cake, you don’t just shout
“Cake!” and expect one to materialize, no matter how specific you get
with your declaration (“with strawberry icing and a caramel filling!”). This
would be the declarative approach, and in practice, it sounds more than
a little eccentric. To bake a cake, you follow a series of well-defined steps
or instructions and have your ingredients and your oven at the ready. This
is akin to the imperative approach in programming; it’s more hands-on,
and sometimes things get messy. But ultimately it gives you more creative
control.
Generating SVG
So if native SVG doesn’t allow for the use of algorithms, how do we write
SVG using an imperative approach? The answer is we script our SVG, and
this is where JavaScript and SvJs come into play.
We could script SVG directly in JavaScript without a library, but that
too has its challenges, the main one being the verbose boilerplate code
we’d have to write. The SvJs library saves us that trouble, making SVG more
intuitive and fun to write. Here’s an example of a simple SVG (Figure 1-2)
written using vanilla JavaScript:
CHapTer 1 THe BeGinner’S paTH
6
const svg = document.createElementNS('<http://www.w3.org/2000/
svg>', 'svg');
svg.setAttribute('width', '150px');
svg.setAttribute('height', '150px');
const div = document.getElementById('container'); div.
appendChild(svg);
const rect = document.createElementNS('<http://www.w3.org/2000/
svg>', 'rect');
rect.setAttribute('x', '0');
rect.setAttribute('y', '0');
rect.setAttribute('width', '150');
rect.setAttribute('height', '150');
rect.setAttribute('fill', 'cornflowerblue');
svg.appendChild(rect);
And the following snippet is the equivalent SVG written using
SvJs (don’t worry about the details just yet; all you need to note is how
concise it is vs. vanilla JavaScript). The output of this code you can see in
Figure 1-2.
const div = document.getElementById('stage');
const svg = new SvJs().set({ width: '150px', height: '150px'
}).addTo(div);
svg.create('rect').set({
x: 0, y: 0, width: 150, height: 150, fill: 'cornflowerblue'
});
CHapTer 1 THe BeGinner’S paTH
7
Figure 1-2. A cornflower blue-colored rectangle, in all its glory
Now you could write some functions to make writing vanilla JavaScript
less painful, but that leads you down the road of writing a whole host of
other utility functions to make the basics less burdensome. With SvJs, I’ve
done my best to save you this trouble. It’s essentially a very thin wrapper
over the real SVG spec with some helpful generative functions thrown in.
This keeps its footprint extremely light while maintaining fidelity to the
SVG spec.
SvJs was inspired by the gySVG library, a similarly light but more
general-purpose JavaScript library that comes complete with a plug-in API
and modern framework support. I was initially going to use gySVG and
extend its functionality with a plug-in, but this plug-in soon grew to the
point where it made more sense to write my own library with a specific
focus on generative art. This was how SvJs came to be.
CHapTer 1 THe BeGinner’S paTH
8
Getting Set Up
Enough with the preamble. Let’s get ourselves set up to write some code.




