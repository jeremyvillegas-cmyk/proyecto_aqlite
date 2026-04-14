<?php
$db = new PDO('sqlite:database.db');

$db->exec("CREATE TABLE IF NOT EXISTS tareas ( 
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT,
    descripcion TEXT
)");
?>

<form method="POST">
    <input type="text" name="nombre" placeholder="Nombre de la tarea" required>
    <br><br>
    <textarea name="descripcion" placeholder="Descripcion"></textarea>
    <br><br>
    <button type="submit">Guardar</button>
</form>

<?php 
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $stmt = $db->prepare("INSERT INTO tareas (nombre, descripcion) VALUES (?,?)");
    $stmt->execute([$_POST['nombre'], $_POST['descripcion']]);
}

$result = $db->query("SELECT * FROM tareas");
foreach ($result as $row) {
    echo "<p><strong>" . htmlspecialchars($row['nombre']) . "</strong>: " . htmlspecialchars($row['descripcion']) . "</p>";
}
?># proyecto_aqlite
