## Add a Button to Movies Page
In the `movies.html` add a button
```html
<a href="/add_movie"><button>Add Movie</button></a>
```
## Create the HTML Form
   - **Template (`add_movie.html`)**:
```html
     <!-- Jinja Extends code -->
         <h1>Add a New Movie</h1>
         <form action="/add_movie" method="post">
      <label for="title">Title:</label>
      <input type="text" id="title" name="title" required><br>

      <label for="year">Year:</label>
      <input type="number" id="year" name="year" required><br>

      <label for="genre">Genre:</label>
      <input type="text" id="genre" name="genre" required><br>

      <label for="director">Director:</label>
      <input type="text" id="director" name="director"><br>

      <label for="cast">Cast:</label>
      <div id="cast-members">
        <div>
          <select name="cast_member">
            {% for cast in cast_members %}
              <option value="{{ cast._id }}">{{ cast.name }}</option>
            {% endfor %}
          </select>
          <input type="text" name="role" placeholder="Role">
        </div>
      </div>
      <button type="button" onclick="addCastMember()">Add Another Cast Member</button><br>

      <button type="submit">Add Movie</button>
    </form>
    <script>
      function addCastMember() {
        var castDiv = document.getElementById('cast-members');
        var newCast = document.createElement('div');
        newCast.innerHTML = \`
          <select name="cast_member">
            {% for cast in cast_members %}
              <option value="{{ cast._id }}">{{ cast.name }}</option>
            {% endfor %}
          </select>
          <input type="text" name="role" placeholder="Role">
        \`;
        castDiv.appendChild(newCast);
      }
    </script>
    <!-- Jinja extends end -->
```

## Handle Form Submission in Flask
   - **Route to Display Form:**
     ```python
     @app.route('/add_movie')
     def add_movie():
	     cast_members = mongo.db.cast.find()
         return render_template('add_movie.html', cast_members=cast_members)
     ```

   - **Route to Handle Form Submission:**
     ```python
     @app.route('/add_movie', methods=['POST'])
	def add_movie_post():
	    title = request.form['title']
	    year = request.form['year']
	    genre = request.form['genre']
	    director = request.form.get('director')
	
	    cast_members = request.form.getlist('cast_member')
	    roles = request.form.getlist('role')
	
	    cast = []
	    for cast_member, role in zip(cast_members, roles):
	        cast.append({
	            '_id': ObjectId(cast_member),
	            'role': role
	        })
	
	    movie = {
	        'title': title,
	        'year': year,
	        'genre': genre,
	        'director': director,
	        'cast': cast,
	        'reviews': []
	    }
	
	    mongo.db.movies.insert_one(movie)
	    return redirect('/movies')
     ```
