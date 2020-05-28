We create the static app with dockerfile just following the instructions below

## Task Create the Index.html

```
cat <<EOF >> index.html
<!DOCTYPE html>
<html lang="en">

<head>
  <title>Vibhuvi</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/js/bootstrap.min.js"></script>

</head>
<body>

<div class="jumbotron">
  <h1>Vibhuvi</h1> 
  <p>Anything and Everything as container</p> 
</div>
</body>
</html>
EOF
```{{execute}}

Check the content of the `index.html`

    `cat index.html`{{execute}}


## Create the Dockerfile

We have many options to deploy HTML static pages, best practice is to create a Dockerfile for any application framework. So we'll create `Dockerfile` 

```
cat <<EOF >>Dockerfile
FROM nginx:1.17.10
COPY . /usr/share/nginx/html
EOF
```{{execute}}

Check the content of the Dockerfile
    `cat Dockerfile`{{execute}}
