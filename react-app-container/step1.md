We create the static app with dockerfile just following the instructions below

## Task Create the ReactApp

```
npx create-react-app my-app
```

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

Check the content `cat index.html`{{execute}}
