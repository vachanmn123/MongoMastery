## Basics of Jinja2
- **What is Jinja2?**
  - A templating engine for Python that generates dynamic HTML or other text formats.
- **Integration with Flask:**
  - The default templating engine in Flask, allowing seamless dynamic content generation.

**Key Features:**
- **Template Inheritance:**
  - Promotes code reuse by defining a base template and extending it in other templates.
- **Control Structures:**
  - Supports conditional statements (`if`, `if-else`) and loops (`for`).

## Control Structures

1. **If Statement:**
   ```html
   {% if user %}
     <p>Welcome back, {{ user }}!</p>
   {% endif %}
   ```

2. **If-Else Statement:**
   ```html
   {% if user %}
     <p>Welcome back, {{ user }}!</p>
   {% else %}
     <p>Hello, Guest! Please log in.</p>
   {% endif %}
   ```

3. **For Loop:**
   ```html
   <ul>
     {% for item in items %}
       <li>{{ item }}</li>
     {% endfor %}
   </ul>
   ```

## Template Inheritance

1. **Base Template (`base.html`):**
   ```html
   <!doctype html>
   <html>
     <head>
       <title>{% block title %}My Website{% endblock %}</title>
     </head>
     <body>
       <header>
         <h1>My Website Header</h1>
       </header>

       <main>
         {% block content %}{% endblock %}
       </main>

       <footer>
         <p>My Website Footer</p>
       </footer>
     </body>
   </html>
   ```

2. **Child Template (`index.html`):**
   ```html
   {% extends "base.html" %}

   {% block title %}Home - My Website{% endblock %}

   {% block content %}
     <h2>Welcome to the Home Page</h2>
     <p>This is the content of the home page.</p>
   {% endblock %}
   ```

## Benefits of Jinja2
- **Separation of Concerns:**
  - Separates application logic from presentation logic.
- **Reusability:**
  - Reuse common layout elements, enhancing consistency and maintainability.

Jinja2 makes it easy to generate dynamic, reusable, and maintainable HTML by providing powerful features like template inheritance and control structures.