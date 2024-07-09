## Implementation of Review creation
Add a add review button on the movie information page
```html
<a href="/movies/<!-- Movie ID -->/add_review"><button>Add Review</button></a>
```
### Create the HTML Form:
   - **Form Fields**: User, Rating, Comment.
   - **Template (`add_review.html`)**:
```html
<!-- Jinja extends -->
         <h1>Add a New Review for <!-- Jinja Movie Name --></h1>
         <form action="/movies/(jinja movie id)/add_review" method="post">
           <label for="user">User:</label>
           <input type="text" id="user" name="user" required><br>

           <label for="rating">Rating:</label>
           <input type="number" id="rating" name="rating" min="1" max="5" required><br>

           <label for="comment">Comment:</label>
           <textarea id="comment" name="comment"></textarea><br>

           <button type="submit">Add Review</button>
         </form>
<!-- Jinja close -->
```

### Handle Form Submission in Flask
   - **Route to Display Form:**
     ```python
     @app.route('/movies/<movie_id>/add_review')
     def add_review(movie_id):
         movie = mongo.db.movies.find_one({'_id': ObjectId(movie_id)})
         return render_template('add_review.html', movie=movie)
     ```

   - **Route to Handle Form Submission:**
     ```python
     @app.route('/movies/<movie_id>/add_review', methods=['POST'])
     def add_review_post(movie_id):
         user = request.form['user']
         rating = request.form['rating']
         comment = request.form.get('comment')

         review = {
             'user': user,
             'rating': rating,
             'comment': comment
         }

         mongo.db.movies.update_one(
             {'_id': ObjectId(movie_id)},
             {'$push': {'reviews': review}}
         )
         return redirect(f'/movies/{movie_id}/view_reviews')
     ```

## Implementation of Cast creation

### Create the HTML Form to Add Cast
   - **Form Fields**: Name, Date of Birth.
   - **Template (`add_cast.html`)**:
     ```html
     <!-- Jinja extends code -->
         <h1>Add a New Cast Member</h1>
         <form action="/add_cast" method="post">
           <label for="name">Name:</label>
           <input type="text" id="name" name="name" required><br>

           <label for="date_of_birth">Date of Birth:</label>
           <input type="date" id="date_of_birth" name="date_of_birth" required><br>

           <button type="submit">Add Cast Member</button>
         </form>
       <!-- End Jinja -->
     ```

### Handle Form Submission in Flask
   - **Route to Display Form:**
     ```python
     @app.route('/add_cast')
     def add_cast():
         return render_template('add_cast.html')
     ```

   - **Route to Handle Form Submission:**
     ```python
     @app.route('/add_cast', methods=['POST'])
     def add_cast_post():
         name = request.form['name']
         date_of_birth = request.form['date_of_birth']

         cast_member = {
             'name': name,
             'date_of_birth': date_of_birth
         }

         mongo.db.cast.insert_one(cast_member)
         return redirect('/')
     ```