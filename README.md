# Hi there! 👋

📚 Welcome to my Hugo Learning Diary. In this repository, I will track my learning progress, take notes for future reference, and gather a knowledge base to build my own portals using Hugo.

## 🚀 Learning Journey

**🗓️ January 24, 2024**

1. **Creating a Hugo Site**
   - Initialize a new Hugo site using the command:
     ```bash
     hugo new site learn-hugo
     ```

2. **Version Control Setup**
   - Create a `.gitignore` file.
   - Push the repository to Git.

3. **Getting Started with Hugo**
   - Beginning Steps: To learn the basics, I'm starting with this guide: [Make a Hugo Blog From Scratch](https://zwbetz.com/make-a-hugo-blog-from-scratch/). I'll try to follow it initially to grasp the fundamental concepts.

**🗓️ January 25, 2024**

1. **Home Page Template**
   - It looks like we need to start with the home page template. Learn more at [Hugo's homepage template guide](https://gohugo.io/templates/homepage/#readout).
     > The homepage template is the only required template for building a site and therefore useful when bootstrapping a new site and template. It is also the only required template if you are developing a single-page website.
   - Also, learn about Lookup rules at [Hugo's template lookup order](https://gohugo.io/templates/lookup-order/).
   - I am modifying a bit of what is said here. I don't like the idea of adding params with content to the site config. I am going to create a content file in the next step. Create a file *layouts/index.html* with the following content:
     ```html
     <!doctype html>
     <html lang="en">
       <head>
         <meta charset="utf-8">
         <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
         <link rel="stylesheet"
         href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css"
         integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS"
         crossorigin="anonymous">
         <title>{{ .Site.Title }}</title>
       </head>
       <body>
         <div class="container">
           <main id="main">
             <div id="home-jumbotron" class="jumbotron text-center">
               <h1>{{ .Site.Title }}</h1>
               <p class="font-125">{{ .Content }}</p>
             </div>
           </main>
         </div>
       </body>
     </html>
     ```
     - `.Site.Title` is a title value from the Hugo site configuration (hugo.toml).
     - `.Content` is the content of a homepage from the `_index.md`. I am creating it in the next step.

2. **Home Page Content (_index.md)**
   - **Front matter** is metadata attached to a content file (yaml, toml, json at the top of a file).
   - Learn about `_index.md` file at [Hugo's content organization guide](https://gohugo.io/content-management/organization/#index-pages-_indexmd).
   - Create this page by using the command: 
     ```bash
     hugo new _index.md
     ```
     and then add content to it.

3. **Site Configuration (hugo.toml)**
   - Add a title to the hugo.toml file, which is the site configuration file.
   - Start the site and test it. Run the command:
     ```bash
     hugo server
     ```
     and browse to the provided URL.

**🗓️ January 26, 2024**

1. **Bootstrap**
   - Today I am going to play with static content for Hugo. I've just realized I need to take a look at Bootstrap. Adding to-do list to the end of this thread.

2. **Static dir in HUGO**
   - I've put the CSS from [here](https://raw.githubusercontent.com/zwbetz-gh/make-a-hugo-blog-from-scratch/master/static/css/bootstrap.min.css) into the file `static/css/bootstrap.min.css`.
   - I've replaced the CDN URL to the Bootstrap CSS in the `layouts/index.html` with content from my static directory, here is the new code:
     ```html
     {{ $css := "css/bootstrap.min.css" | relURL }}
     <link rel="stylesheet" href="{{ $css }}">
     ```

3. **Single Page Layout**
   - Layout for our single pages (posts) will be here: `layouts/_default/single.html`. It contains the following content:
     ```html
     <!doctype html>
     <html lang="en">
       <head>
         <meta charset="utf-8">
         <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
         {{ $css := "css/bootstrap.min.css" | relURL }}
         <link rel="stylesheet" href="{{ $css }}">
         <title>{{ .Title }}</title>
       </head>
       <body>
         <div class="container">
           <main id="main">
             <h1>{{ .Title }}</h1>
             {{ .Content }}
           </main>
         </div>
       </body>
     </html>
     ```
   - In the `archetypes` directory, we have a list of 'templates' with different types of content. Let's try to edit `draft = true` to `draft = false`.
   - The next one may be a good idea. Let's change the default URL for posts from `/blog/:filename:` to just `/:filename:`. Edit site config `hugo.toml`:
     ```toml
     [permalinks]
       blog = "/:filename/"
     ```
   - Create a new page with the command:
     ```bash
     hugo new blog/first-page.md
     ```
   - Adding tags to this page's front matter:
     ```
     tags = ["anime", "one piece"]
     ```
   - Adding the content. I've added some static files to the assets directory so Hugo can process them. They are used in the `first-page.md` file.
   - To display images with my custom formatting and to process them via Hugo, let's create our own shortcode. Create a file `layouts/shortcodes/img.html`. Now I can use this shortcode in my Markdown file.

**🗓️ January 27, 2024**

1. **Baseof Layout**
   - Now I think it was better to start with `layouts/_default/baseof.html`. It is a default template for any other pages like homepage or single page. Let's create it now and move the base HTML code to it.
   - Look at that file, there we have:
     ```
     {{ block "main" . }}{{ end }}
     ```
     This piece of code defines a block named "main". The `.` symbol passes the current context to the block. Now, for example, we can edit `single.html`, the `{{ define "main" }}` section will override the "main" block from `baseof.html` with the specific content for a single page.

2. **Partials Layout**
   - Learn about partials: [Partials in Hugo](https://gohugo.io/templates/partials/#readout). Here you can define footer, header, head parts of your pages.
   - I've created a directory `layouts/partials/head.html` with the head component. And then instead of having this code in the `baseof.html`, I've added a calling of this partial: `{{ partial "head.html" . }}`.

3. **List Layout**
   - List layout is a layout for parent pages. I've created two more pages with content to have a set of pages.
   - I've created a list template `layouts/_default/list.html`.
   - I've added my own styles to `layouts/_default/list.html` and put them in the `assets/css/list.css` file.

4. **Menus**
   - Read about menu templates in Hugo here: [Menu Templates in Hugo](https://gohugo.io/templates/menu-templates/#readout).
   - I've created a menu component at `layouts/partials/nav.html`.
   - This component has been added to the `baseof.html` template.
   - SVG icons have been added as assets, allowing them to be processed by the Hugo engine. In `nav.html`, the menu configuration is read, and icons are set using the 'pre' configuration key.


## To-Do List 📝

### Tasks
🔲 **Get familiar with Bootstrap**

🔲 **How to add Bootstrap JS to your HUGO portal?**

### Completed Tasks
✅ **Completed Task Name**

*Stay tuned for updates as I progress through my Hugo learning journey!* 🌟 🌈 🦄