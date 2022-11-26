## Proyecto que se realiza en Android: Volley + PHP + Mysql

conexion.php
```
<?php

function retornarConexion(){
	$servername = " ";
	$username = " ";
	$password = " ";
	$dbname = " ";

	// Create connection
	$conn = new mysqli($servername, $username, $password, $dbname);
	// Check connection
	if ($conn->connect_error) {
	  die("Connection failed: " . $conn->connect_error);
	}
	return $conn;
}

?>

```

## listar3.php
```
<?php
require("conexion.php");

$conn = retornarConexion();

$sql = "SELECT codigo,descripcion,precio FROM articulos";
$result = $conn->query($sql);
$miresult=mysqli_fetch_all($result,MYSQLI_ASSOC);
echo json_encode($miresult);
$conn->close();
?>
```

## insertar.php
```
<?php
header('Content-type=application/json; charset=utf-8');
$datos = json_decode(file_get_contents("php://input"),true);



require("conexion.php");

$conn = retornarConexion();


$sql = "insert into articulos (codigo,descripcion, precio) values ('$datos[codigo]','$datos[descripcion]','$datos[precio]')";
//echo $sql;
if ($conn->query($sql))
	echo '{"respuesta":"ok"}';
else
	echo '{"respuesta":"error en la insercción"}';

$conn->close();

?>
```



