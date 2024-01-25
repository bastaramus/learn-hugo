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



*Stay tuned for updates as I progress through my Hugo learning journey!* 🌟 🌈 🦄