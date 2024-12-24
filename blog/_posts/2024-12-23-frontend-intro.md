---
layout: post
title: A no-nonsense guide to frontend for backend developers
lang: english
categories: [ blog ]
description: A comprehensive guide to frontend frameworks and libraries. 
tags: programming 
image: assets/img/frontend/featured_pen.jpg
---

<ul>
  <li><a href="#introduction">Introduction</a></li>
  <li><a href="#absolute-basics">Absolute basics</a></li>
  <li><a href="#client-side-vs-server-side">Client-side vs. Server-side</a></li>
  <li><a href="#components">Components</a></li>
  <li><a href="#frontend-libraries">Frontend libraries</a></li>
  <li><a href="#conclusion">Conclusion</a></li>
</ul>

<a id="introduction"></a>
## Introduction
I am a backend developer... the usual kind... the kind that is good at math but terrible at aesthetics. Any attempt at design that I ever made always resulted in boring looking generic junk. I tried using dozens of tools but the end result would always look like it was written in *Microsoft FrontPage 2003*

I was self-conscious enough to see that, so I gave up trying. I will write you a document, but only if you give me a ready $\LaTeX$ style file. I will write a blog, but only in *Markdown* and let someone else worry about visual appeal. I will prepare a *DevFest* presentation, but only if organizers provide a *PowerPoint template*. I will never try to design anything, be it a button or a sign-in form.

And yet, I cannot just shave my head and retreat to backend `JSON API` sanctuary --- I still need to write frontend for my pet projects and build dashboards for internal use. But trying to enter the frontend world is incredibly painful --- dozens of frameworks, libraries, philosophies. I have been hearing the words `React` or `Angular` or `Node` for the last 8 years but I was too scared to actually try and make sense of them. Learning `C++` or *Leetcode* has been easier than this.

Nevertheless, I forced myself to learn it, and now I want to be a Prometheus (I am not sure if there isn't already a `JS` framework with this name) and bring this knowledge to my people --- the backend devs.

As a bonus, I included the ultimate recommendation of which frontend framework to choose. I myself had a decision paralysis for a very long time and this will help you overcome it and start building things without overthinking it. 

<a id="absolute-basics"></a>
## Absolute basics
Let's start with the absolute basics to ensure that we are on the same page before discussing frameworks. You can skip this section if you want.

### Minimal web page
A minimal web page consists of a text file with extension `.html` and tags for content:

```html
<html>
	<div>Hello World!</div>
</html>
```

To add formatting you can either add a style attribute:

```html
<html>
	<div style="color:red; font-size:20px">Hello World!</div>
</html>
```

or if you have a lot of formatting, add `id` to your content and refer to it from `<style>` tag. The style is formatted using `CSS` language which looks like an `HTML` element followed by `JSON` related to it:

```html
<html>
	<div id="mytext">Hello World</div>

	<style>
		/* CSS code */
		#mytext {color:red; font-size:20pt} 
	</style>
</html>
```

This will create static pages that do not change and do not react to any events. To add some interactivity, like checking if you left a form field empty or entered a valid email, you will need `JavaScript`.

### Running JavaScript
Before using any programming language you must first install it on your computer. For `C/C++` you need to install a compiler like `GCC` or `Clang`, for `Python` you need to install a `CPython` interpreter.

To run `JavaScript` you only need a web browser --- all modern web browsers can run `JS` code. It is as simple as opening a web browser and going to pressing `F12`. This will open a `JS` console:

<figure class="d-flex justify-content-center">
	<img src="/assets/img/frontend/browser_console.png" alt="Web browser console"/>
</figure>

You can also create a text file with extension `.html`  and put a `<script>` tag on it, open this file in browser, and the outcome will be displayed if you press `F12`:

```html
<!-- myfile.html -->
<html>
	<script>
		// write a JS code here
		console.log('Hello World');
	</script>
</html>
```

However, for safety reasons, the browser console has no access to your file system and lacks some other features that would make it possible to use `JS` to, at least, achieve the functionality of other scripting languages like `Python` or `Ruby`. So, there is a second way to run `JS` code on your computer --- installing `Node.js`. It is essentially a `JS` interpreter which can do stuff like reading and writing files:

```js
//$ node
//Welcome to Node.js v23.3.0.
//Type ".help" for more information.
> console.log('Creating a new directory');
> fs.mkdirSync('new_dir'); // access filesystem using fs
```

With `Node.js` you can run `JS` code in the server or in your `Docker` container without having to install a web browser. We will see below that this is very useful.

### Classical stack
Combining the sections above we can create a web page using the classical `HTML+CSS+JS` setup.

They can be combined in a single `.html` file with 3 sections: content itself, styles, and scripts:

```html
<html>
	<!-- page HTML content here -->
	<div id="mytext">Hello World</div>
	<button onclick="sayHelloWorld()">Say Hello</button>
	
	<style>
		/* page CSS styles here */
		#mytext {color:red; font-size:20pt}
		button {font-size: 40pt}
	</style>
	
	<script>
		// page JS scripts here
		function sayHelloWorld() {
			console.log('Hello World');
		}
	</script>
</html>
```

You can see that we have a button that triggers a function `sayHelloWorld()`, which is defined inside  `<script>` tags and it has font size of `40pt`, which is defined inside `<style>` tags.

Also note that the comment symbols are different in all 3 sections:
- inside pure `HTML` it is `<!-- -->`
- inside `CSS` it is `/* */`
- inside `JS` it is `//`.

This shows that the browser understands that these are 3 different languages. So, the usual practice is not to clutter `.html` file too much and separate it into 3 files and call styles and scripts by file path:

**content.html**
```html
<html>
	<div id="mytext">Hello World</div>
	<button onclick="sayHelloWorld()">Say Hello</button>

	<!-- include styles -->
	<link rel="stylesheet" type="text/css" href="styles.css" />

	<!-- include scripts -->
	<script src="scripts.js"></script>
</html>
```

**styles.css**
```css
#mytext {color:red; font-size:20pt}
button {font-size: 40pt}
```

**scripts.js**
```js
function sayHelloWorld() {
	console.log('Hello World');
}
```

The biggest problem with this setup is that if you look at the `HTML` element, for example, the `<button>`, you cannot know which style it has and which scripts are listening to it unless you look at the other two files. Similarly, if you look at the `.js` file, you see a function `sayHelloWorld()` but have no idea whether it is needed or not, or if some element is calling it or not, without looking at the `.html` file. This goes against the so-called *Locality of Behavior* principle.

Anyway, this setup has been used on the Web for several decades.

<a id="absolute-basics"></a>
## Client-side vs. Server-side
Great! We have covered the basics. Now let's talk about the main dilemma that underlies all discussions regarding the choice of a frontend framework, and the architecture of your app in general. Before we start, let's clarify some terminology: *client-side* means the browser or an app in which the users consume your content, and *server-side* is usually the backend server that stores the login information, has access to database, and overall serves as the backbone of the entire app. Now we are ready to dive deeper.
### Classical HTML generation
In any non-trivial web app that displays any kind of data we will need a way to generate `HTML` scripts automatically. Otherwise, whenever the data is updated, somebody will have to manually update the `HTML` tags.

Since `HTML` is a simple text file, it can be easily created by any scripting language as a string. There are many libraries that do this. For example, with `Jinja2` library we can write all elements of a list `mylist = [1,2,3,4,5]` into table rows using a language that resembles `Python`:

```jinja2
<table>{% raw %}
	{% for item in mylist %}
		<tr> <td> {{ item }} </td> </tr>
	{% endfor %}{% endraw %}
</table>
```

Of course, the browser would not understand this --- you will need to *render* this `Jinja2` script into actual `HTML` by running special commands in `Python`, which will render an `.html` file:
```html
<table>
	<tr> <td> 1 </td> </tr>
	<tr> <td> 2 </td> </tr>
	<tr> <td> 3 </td> </tr>
	<tr> <td> 4 </td> </tr>
	<tr> <td> 5 </td> </tr>
</table>
```

This feature is so crucial that it even has a special name --- *templating*. I want to stress one thing: such `HTML` generation from a template happens in the server in a language of your choice (`Python/Ruby/Java/C#`), usually a language your backend code is written in. Browsers do not understand  these languages natively --- they only understand `JS`, so we send them a pre-rendered `HTML` file. This will become important later on. 


### JSON vs HTML API
In the previous section we saw how backend can generate `HTML` scripts and fill them with the data from database and other information. For example, if the user presses the *Like* button on some social media post, the backend must update the content of *Liked Posts* page to include that new post there. This can be done in two ways:

**1)** Backend has an `HTML` template ready with some `Jinja2` script and renders it with the latest query result from the database:

```jinja2
<table>{% raw %}
	{% for post in liked_posts %}
		<tr><td>{{ post.author }}</td><td>{{ post.text }}</td></tr>
	{% endfor %}{% endraw %}
</table>
```

Here the rendered `HTML` is sent directly to the frontend together with the `CSS` styles and `JS` scripts. The browser simply displays what the backend has already prepared and is not aware of the types of data or any logic on the page.

**2)** Backend sends the `JSON` that specifies the query result from database 's `liked_posts` table in a format that browser would understand:
```JSON
{
	liked_posts: [
			{author: "Apple", text: "Think different"},
			{author: "Nike", text: "Just do it"}
		]
}
```

The browser runs special `JS` functions that request such `JSON`, and when they receive it, they use extract data from it and generate `HTML` from it on the browser itself:

```html
<table id="myTable"></table>

<script>

	// Find the table
	const table = document.getElementById('myTable');
	
	// For each entry in JSON add a row with two columns for author and text
	liked_posts.forEach(post => {
		table.innerHTML +=
			"<tr><td>" + post.author + "</td><td>" + post.text + "</td></tr>";
		});
		
</script> 
```

### Server-side rendering

Note that in `JSON API` architecture the browser knows a lot about the data it receives --- it sees the different fields, it can perform programming tasks on it like reversing strings, multiplying, repeating, reusing the author name in several places etc.

This is really useful if you need a complex interactive user interface but this is slightly less secure because the browser is not in your hands --- it belongs to a user who can be malicious. 

Moreover, if the user's computer is weak, running all these scripts in the browser will slow down the entire web app, unlike pre-rendered `HTML` which is a simple text file that will run smoothly in most computers.

Also, the search engine crawlers do not usually wait for the web page to load all of its scripts, and if the page has zero content on it to begin with, the search engine optimization suffers as a result.

There is a modern trend called *Server-side rendering (SSR)* that runs `Node.js` on the server and pre-renders some `HTML` pages using `JS` directly in the server. This kinda solves the problems above, but it also bites a slice of the backend's pie. If we try to visualize the three approaches, it would be something like this (assuming backend is in `Python`):

<figure>
	<img src="/assets/img/frontend/clientserver.png" />
</figure>

In SSR the `Python` backend has access to database and maybe stores login information, but everything else is done in `JS`. The diagrams are very simplistic, but in SSR there is also `JS` on the client side, making the entire web application 95% written in `JS`. Some libraries took the next logical step and covered the entire backend in `JS` using frameworks like `Express.js`, but I won't be talking about the `JS` backend in this article.

### Build step
These `JS` scripts are usually not written manually but are compiled by some higher level `JS` library or framework. This build step (i.e. compilation of higher level code into `HTML+JS`) is done in server using a running `Node.js` instance.

By design, all the `JS` dependencies are installed into a virtual environment (similar to `virtualenv` in Python or `rbenv` in Ruby) that is stored directly in the work folder in a subdirectory called `node_modules`. It usually takes up around 200MB of space and should be `.gitignored`.

Once you run a build command that usually looks like `npm run build`, it will generate the static `HTML+JS` files. Now you have 2 options to serve these static files to the client's browser:

1. Using your backend's `FileResponse` which simply scans for the generated files in the static directory, resolves the relative paths, and sends the files to the client.
2. Using `Node.js`'s  serve functionality like `npx serve mydir` which will run a server in a separate port, independently from your backend.

Overall, it looks kinda like this:

<figure>
	<img src="/assets/img/frontend/servestatic.png" />
</figure>

Option 1 has a very intuitive setup --- you can bind your backend's router and respond to certain URLs with these files.

```python
@app.get("/")
def index():
	return FileResponse("dist/index.html")
```

Option 2 is popular for some reason, although it is more complicated. In this setup you only expose the frontend port to the client, and it will serve the static `HTML+JS` app without any need for the backend. And only when it needs to fetch data from the backend, will the frontend connect to the backend itself, abstracting away this functionality from the browser. Of course, to do so the frontend now will need its own router. Basically, this is frontend trying to do what backend should be doing.

<a id="components"></a>
## Components
So far, we have covered the basics of how the working frontend code can be written and where it is located. We have seen how `HTML` can be automatically generated but, up till now, we assumed that the `JS` part is written manually. This is very often not the case in the real life frontend development. Manually writing `JS` scripts is cumbersome and your code structure gets very messy very fast. Moreover, if you need to reuse scripts, you will have to old-school copy and paste them. So, since the very beginning, developers used some sorts of libraries to make `JS` development easier and more structured.

### JQuery
In the early days, using vanilla `JS` to find and modify elements or to send `AJAX` requests to the server was very cumbersome. Thus, many developers used `JQuery`, which was a neat syntactic sugar on top of the vanilla `JS`. Many add-ons have been written in `JQuery`, like `Datatables` (interactive tables with search, pagination, sorting out of box), or animated clocks, or counters etc. Using such components pre-written by someone else was really easy --- just download the code and add it to your `HTML` page under `<script>` tags. Revisiting the example from above, we could add a row to a table much easier with `JQuery`:

```js
 // const table = document.getElementById('myTable');
	const $table = $('#myTable');
		
//	table.innerHTML += "abc";
	$table.append("abc");
```

or sending an `AJAX` request to the backend API would require an entire separate library for vanilla `JS` while it could be done easily in `JQuery`:

```js
$.ajax({ url: 'api.example.com', method: 'GET'});
```

With time, though, vanilla `JS` and `HTML` standard itself added a lot of functionality, making `JQuery` kinda obsolete. For example, pop-up calendars to select dates are built-in in HTML nowadays. Still, a lot of current web depends on `JQuery` in one way or another.

### Bootstrap
Around 2010, `Bootstrap` was created as a library of reusable components, such as beautiful buttons, responsive forms, and pop-ups. The main feature of `Bootstrap` was that it relied on the `HTML` syntax, trying to minimize the time and energy the developers spend writing actual `JS` code. It used `JQuery` and `CSS` under the hood, but it completely abstracted it away for its users. Basically, using `Bootstrap` was as simple as adding classes to the `HTML` elements.

For example, you want to write a button which shows or hides a text when pressed. In `JS` this looks like:

```html
<!-- button itself -->
<button id="myButton">Toggle Text</button>
<!-- target text -->
<div id="text" style="display:none;">
	Example text here.
</div>

<script>
	// find the button
	const myButton = document.getElementById('myButton');

	// when the button is clicked:
	myButton.onclick = () => {
		// find the target text with id=text
		const el = document.getElementById('text');
		// change display:none to display:block
			el.style.display = el.style.display === 'none' ? 'block' : 'none';
		};
</script>
```

But in Bootstrap you do not write a single line of `JS` yourself, just put the necessary classes:

```html
<!-- Button here targets #text and collapses it -->
<button data-bs-toggle="collapse" data-bs-target="#text">Show/hide</button>

<!-- Text with id #text -->
<div class="collapse" id="text">
	Example text here.
</div>
```

Bootstrap was a revolution in frontend development, and many libraries followed its approach, like `PicoCSS` or `TailwindCSS`. It super-powered the `HTML` by just adding classes to it, but it couldn't create custom `HTML` elements and had to rely on native `HTML` elements.

```html
<!-- This will work -->
<button class="btn">Custom Button</button>

<!-- This will not work, because HTML does not have <btn> element -->
<btn>Custom Button</btn>
```

This means that you couldn't really create easy-to-use complex components like `<PieChart />` or `<InteractiveTable />`. 
### JSX and the likes
Around the same time another approach to writing frontend appeared --- using scripting capabilities of `JS` to develop components of any complexity and then simply compile them into `HTML` (also known as the *Build step*). To be able to do this, `React.js` (and other similar libraries) found a way to write `HTML` components inside the `JS` code. There are multiple ways to do this, but I will show just one of them, called `JSX`, which works like this:

```jsx
function btn() {
	// inside this JSX function we can write HTML and JS together
	return (
		<button style="..." onclick="...">Custom Button</button>
	);
}
```

and then use it inside a main `JSX` function:

```jsx
function App() {
	return (
		<div>
			<btn> </btn> // custom component <btn> defined in btn() function
		</div>
	);
}
```

The web browser would not understand this `<btn>` element, so the final step is to compile this `JSX` code into `HTML+JS`. The result will be something like:

```html
<div id="root"></div>

<script>
	// find root div, transform it using JS....
</script>
```

The principle is very similar to compiling scripts to machine code. The end result will not be human-readable, and the resulting `HTML` will contain lots of `<script>` tags instead of clear elements like `<div>` or `<button>`. Below is a side-by-side comparison of the sources of Twitter (written in `React.js`) and Basecamp (written in `HTML` and a little bit of vanilla `JS`). You can see which of them is easier to read and looks more like `HTML`:

<figure>
	<img src="/assets/img/frontend/basecamp_twitter.png" />
</figure>
 
There are other alternatives to `JSX`, which include `JS` inside `HTML` instead of including `HTML` inside `JS`, but in the end, all of them compile into the pile of non-human-readable scripts that somehow make browser-unsupported components work.

By default, this pile of compiled `JS` scripts is sent to browser, which then renders them. In the Server-Side rendering, the compiled scripts are compiled and rendered in the server, while the browser receives simple `HTML`.
### Web components
As a reaction to the widespread component frameworks like `React.js`, the Web standard has introduced a native way to create custom web components such as `<btn> </btn>` in the example above. Basically, the modern browsers will understand this `JS` code where you define your `<my-btn>` without any 3rd party frameworks.

```html
<!-- use the custom my-btn -->
<my-btn> </my-btn>

<script>
// inherit HTMLElement
class Btn extends HTMLElement {...}
// define <my-btn> as Btn above
customElements.define('my-btn', Btn);
</script>
```

However, this approach didn't really catch on yet.
### JS component libraries
For those people who hesitate using libraries like `React.js`, there are `JS` libraries that provide pre-compiled components like `Chart.js` which you can use to create charts with vanilla `JS`:

```html
<!-- specify where to draw a chart -->
<canvas id="myChart"></canvas>

<script>
	// find canvas
	var ctx = document.getElementById('myChart');
	// draw chart on canvas with data=[1,2,3]
	var myChart = new Chart(ctx, {type: 'bar', datasets: [{ data: [1, 2, 3]}]});
</script>
```

This is really helpful if you need an interactive chart but don't want to go fully into frontend `JS` area. However, you will need to have your data in `JSON` format, because such libraries usually do not read data from `HTML`.


<a id="frontend-libraries"></a>
## Frontend libraries
Finally, let's have a very brief overview of the most popular frontend libraries and frameworks. By library we mean something that can render `JS` and `HTML` with custom components. By framework we mean everything in the library plus a frontend router and state management (i.e. ability to store global variables in the frontend). 
### React.js

*Brief summary:*
Uses `JSX` to add `HTML` into `JS` functions:

```jsx
function App() { return <p>Hello world!</p>; }
```
which is not the most intuitive way to write dynamic pages.

It is a library and supports numerous 3rd party tools for routing and state management. That is why it is too flexible and less intuitive for beginners.

*Verdict:* Not recommended.
### Vue.js

*Brief summary:*
Uses *templates* to add `JS` into `HTML`:

```html
<div id="app">
	<p>Hello, {% raw %}{{ name }}{% endraw %}!</p>
</div>
```
which is very intuitive.

It is a framework with `Vue Router` for routing and `Pinia` for state management. These are very often an overkill for backend developers, so keeping logic outside `Vue` would be wise.

It has a great community and ready-made component libraries for easily building stunning user interfaces --- `PrimeUI` and `Vuetify`.

*Verdict:* Recommended if you need beautiful UI.
### Svelte

*Brief summary:*
A new kid in the block. Uses Single File Component system, where you write styles, scripts, and `HTML` content in one file. Very easy to use.

Uses *templates* like `Vue.js`.

```html
<script>
	// define variable here
	let name = 'World';
</script>

<p>Hello, {name}!</p>
```

It is a minimal framework. And you will find yourself writing a lot of vanilla `JS` code to achieve some functionality that is easy in `Vue.js`

*Verdict:* Not recommended.
### Alpine.js

*Brief summary:* a minimal library that has no build step --- the entire library is a single 15 KB `JS` file.

Uses *templates* like `Vue.js` and `Svelte` but you can write `JS` directly inside `HTML` attributes without any `<script>` environment:

```html
<!-- import library -->
<script src="//unpkg.com/alpinejs"></script>

<div x-data="{ name: 'World' }"> <!-- define name here -->
	<p>Hello, <span x-text="name"/>!</p> <!-- use name here -->
</div> 
```

It markets itself as a modern replacement for `JQuery` and it is really cool for adding a little bit of interactivity without a complicated user interface.

*Verdict:* Recommended if you need a little bit of interactivity and handling JSONs.
## HTMX

*Brief summary:* a library that promotes having all logic in the backend and requesting `HTML` instead of `JSON`. 

Promotes using any backend-side templating library like `Jinja2` to generate required `HTML` and then send this `HTML` snippet to the client without any `JS`.

```html
<div hx-get="/api/name" hx-swap="innerHTML">
	<!--
	sends a GET request to /api/name
	and puts whatever it receives
	inside this current div
	-->
</div>
```

and the backend sends not a `JSON` but an `HTML` snippet:

```python
# on GET request to /api/name return HTML
@app.get("/api/name", response_class=HTMLResponse)
def api_name():
	return "<p>Hello, World!</p>" # instead of {"name": "World"}
```

Supports all `HTTP` verbs (`GET/POST/PUT/PATCH/DELETE`).

*Verdict:* Recommended if you don't need `JSON` data.
### Which framework to choose?
I will try to be as simplistic and dismissive as possible, because if I went into an objective analysis of pros and cons, you wouldn't get any useful information aside from "it depends". I will be biased towards the least movements necessary to set up a user interface. So, here is my ultimate recommendation:

<figure>
	<img src="/assets/img/frontend/frontend_flowchart.png" />
</figure>


<a id="conclusion"></a>
## Conclusion
In this blog post I wanted to share everything that I learned about frontend as a backend developer. It seems that this stuff is overly complicated and intimidating, although, upon digging, I realized that there is a logic and structure to it. I hope that I could convey my understanding to you, and that you found this post useful.
