## Update Operation

### Display the Update Form:**
   - **Purpose**: Provide a form pre-filled with the current movie details.
   - **HTML Template (`edit_movie.html`)**:
     ```html
     <!-- Jinja extends -->
         <h1>Edit Movie</h1>
         <form action="/movies/{{ movie._id }}/update" method="post">
           <label for="title">Title:</label>
           <input type="text" id="title" name="title" value="{{ movie.title }}" required><br>

           <label for="year">Year:</label>
           <input type="number" id="year" name="year" value="{{ movie.year }}" required><br>

           <label for="genre">Genre:</label>
           <input type="text" id="genre" name="genre" value="{{ movie.genre }}" required><br>

           <label for="director">Director:</label>
           <input type="text" id="director" name="director" value="{{ movie.director }}"><br>

           <button type="submit">Update Movie</button>
         </form>
       <!-- Jinja close -->
     ```

### Handle Update Form Submission in Flask:**
   - **Route to Display Update Form:**
     ```python
     @app.route('/movies/<movie_id>/edit')
     def edit_movie(movie_id):
         movie = mongo.db.movies.find_one({'_id': ObjectId(movie_id)})
         return render_template('edit_movie.html', movie=movie)
     ```

   - **Route to Handle Update Submission:**
     ```python
     @app.route('/movies/<movie_id>/update', methods=['POST'])
     def update_movie(movie_id):
         title = request.form['title']
         year = request.form['year']
         genre = request.form['genre']
         director = request.form.get('director')

         mongo.db.movies.update_one(
             {'_id': ObjectId(movie_id)},
             {'$set': {
                 'title': title,
                 'year': year,
                 'genre': genre,
                 'director': director
             }}
         )
         return redirect('/')
     ```

## Delete Operation

### Delete Button in Movie Details Page
   - **HTML Template Snippet:**
     ```html
     <form action="/movies/{{ movie._id }}/delete" method="post" onsubmit="return confirm('Are you sure you want to delete this movie?');">
       <button type="submit">Delete Movie</button>
     </form>
     ```

### Handle Delete Request in Flask
   - **Route to Handle Deletion:**
     ```python
     @app.route('/movies/<movie_id>/delete', methods=['POST'])
     def delete_movie(movie_id):
         mongo.db.movies.delete_one({'_id': ObjectId(movie_id)})
         return redirect('/movies')
     ```
