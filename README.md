# barbearia-dos-guris

codigos usados:

Pagina de cadastro

//<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Cliente - Barbearia Dos Gurizes</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Cadastro de Cliente</h2>
    <form action="processa_cadastro.php" method="POST">
        <label for="nome">Nome:</label>
        <input type="text" id="nome" name="nome" required><br>
        <label for="email">E-mail:</label>
        <input type="email" id="email" name="email" required><br>
          <label for="senha">Senha:</label>
        <input type="password" id="senha" name="senha" required><br>
         <button type="submit">Cadastrar</button>
    </form>
</body>
</html>

Arquivo: processa_cadastro.php
<?php
include('conexao.php');
$nome = $_POST['nome'];
$email = $_POST['email'];
$senha = password_hash($_POST['senha'], PASSWORD_DEFAULT);

$query = "INSERT INTO clientes (nome, email, senha) VALUES ('$nome', '$email', '$senha')";
$result = mysqli_query($conn, $query);

if ($result) {
    echo "Cadastro realizado com sucesso!";
} else {
    echo "Erro ao cadastrar. Tente novamente.";
}
?>

Página de Listagem de agendamentos:


Vamos criar o arquivo listar_agendamentos.php para visualizar os agendamentos:
Arquivo: listar_agendamentos.php

<DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agendamentos - Barbearia Dos Gurizes</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Agendamentos</h2>
    <table>
        <tr>
            <th>Cliente</th>
            <th>Data</th>
            <th>Horário</th>
            <th>Barbeiro</th>
        </tr>
        <?php
        include('conexao.php');
        $query = "SELECT * FROM agendamentos";
        $result = mysqli_query($conn, $query);
        while ($row = mysqli_fetch_assoc($result)) {
            echo "<tr>";
            echo "<td>" . $row['cliente'] . "</td>";
            echo "<td>" . $row['data'] . "</td>";
            echo "<td>" . $row['horario'] . "</td>";
            echo "<td>" . $row['barbeiro'] . "</td>";
            echo "</tr>";
        }
        ?>
    </table>
</body>
</html>

Página de edição/atualização:


Iremos criar os arquivos editar_cliente.php e atualiza_cliente.php para editar informações dos clientes.
Arquivo: editar_cliente.php
<?php
include('conexao.php');
$id = $_GET['id'];
$query = "SELECT * FROM clientes WHERE id='$id'";
$result = mysqli_query($conn, $query);
$row = mysqli_fetch_assoc($result);
?>
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Editar Cliente - Barbearia Dos Gurizes</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Editar Cliente</h2>
    <form action="atualiza_cliente.php?id=<?php echo $id; ?>" method="POST">
        <label for="nome">Nome:</label>
        <input type="text" id="nome" name="nome" value="<?php echo $row['nome']; ?>" required><br>
        
        <label for="email">E-mail:</label>
        <input type="email" id="email" name="email" value="<?php echo $row['email']; ?>" required><br>
        
        <button type="submit">Atualizar</button>
    </form>
</body>
</html>
Arquivo: atualiza_cliente.php
<?php
include('conexao.php');
$id = $_GET['id'];
$nome = $_POST['nome'];
$email = $_POST['email'];
$query = "UPDATE clientes SET nome='$nome', email='$email' WHERE id='$id'";
$result = mysqli_query($conn, $query);
if ($result) {
    echo "Dados atualizados com sucesso!";
} else {
    echo "Erro ao atualizar. Tente novamente.";
}
?>

Página de Exclusão
Basicamente, utilizaremos o arquivo excluir_cliente.php para excluir clientes.
Arquivo: excluir_cliente.php
<?php
include('conexao.php');
$id = $_GET['id'];
$query = "DELETE FROM clientes WHERE id='$id'";
$result = mysqli_query($conn, $query);
if ($result) {
    echo "Cliente excluído com sucesso!";
} else {
    echo "Erro ao excluir cliente. Tente novamente.";
}
?>
O estilo do site:
E, por último, no arquivo styles.css para adicionar estilo às páginas:
Arquivo: styles.css
body {
    font-family: Arial, sans-serif;
    margin: 20px;
    padding: 20px;
}
h2 {
    color: #333;
}
form {
    margin-bottom: 20px;
}
label {
    display: inline-block;
    width: 100px;
}
input {
    margin-bottom: 10px;
    padding: 5px;
}
button {
    padding: 10px 15px;
    background-color: #5cb85c;
    color: white;
    border: none;
    cursor: pointer;
}
table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;//
}
th {
    background-color: #f2f2f2;  }

