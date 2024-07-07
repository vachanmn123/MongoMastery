## Base Page
```html
<!doctype html>

<html lang="en">

<head>

	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>MongoMastery Project</title>
	<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

</head>
<body>

<nav class="navbar bg-dark navbar-expand-lg bg-body-tertiary" data-bs-theme="dark">
	<div class="container-fluid">
		<a class="navbar-brand" href="/">Movie Catalogue</a>
		<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
		<span class="navbar-toggler-icon"></span>
		</button>
		<div class="collapse navbar-collapse" id="navbarNav">
			<ul class="navbar-nav">
				<li class="nav-item">
					<a class="nav-link" aria-current="page" href="/movies">Movies</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" href="/casts">Cast</a>
				</li>
			</ul>
		</div>
	</div>
</nav>
<div style="margin: 1rem;">
<!-- Add Jinja Templating here -->
</div>


<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
integrity="sha384YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
</body>
</html>
```

## Home Page
```html
<!-- Add Jinja extending -->
<h1>Welcome to Movies Catalogue</h1>
<p>Select a page from the top bar to go to the page</p>
<!-- Close Jinja block -->
```
## Movies Listing Page
```html
<!-- Jinja Extends -->

<!-- Jinja block -->
<h1>Movies</h1>
<p>Here are a list of all the movies in the database</p>

<div class="col">
  <!-- Jinja Loop -->
  <div class="card mb-3">
    <div class="card-body">
      <h5 class="card-title">Movie Name</h5>
      <p class="card-text">Sci-Fi</p>
      <a href="#" class="btn btn-primary" style="width: 100%;">View More</a>
    </div>
  </div>
  <!-- Jinja Loop end -->
</div>

<!-- Jinja Block end -->
```

## Movie Information Page
```html
{% extends 'base.html' %}

{% block content %}
<h1><!-- Movie Name --></h1>
<small><!-- Movie year --> - <!-- Movie Genre --></small>
<h2>Cast</h2>
<p><strong>Director:</strong><!-- Movie Director --></p>
<ul>
  <!-- Cast informtation for loop jinja -->
  <!-- <li>Actor Name - Actior Role</li> -->
</ul>
<h2>Reviews</h2>
<ul>
  <!-- Review information for loop jinja -->
  <li>
    <p><strong><!-- Reviewer Name --></strong></p>
    <p>⭐️ <!-- Print number of stars as per review --></p>
    <p><!-- Review Content --></p>
  </li>
</ul>
{% endblock %}
```
