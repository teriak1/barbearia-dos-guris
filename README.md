# barbearia-dos-guris

codigos usados:

(menu.html):
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu - Barbearia Dos Gurizes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
        }
        h1 {
            margin-top: 50px;
            color: #333;
        }
        button {
            width: 200px;
            margin: 10px;
            padding: 15px;
            font-size: 16px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>Bem-vindo à Barbearia Dos Gurizes</h1>
    <button onclick="window.location.href='login.html'">Entrar como Cliente</button>
    <button onclick="window.location.href='loginFuncionario.html'">Entrar como Funcionário</button>
    <button onclick="window.location.href='cadastro.html'">Criar Conta</button>
    <button onclick="window.location.href='ajuda.html'">Ajuda</button>
</body>
</html>

Cadastro(cadastro.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro - Barbearia Dos Gurizes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
        }
        form {
            background-color: white;
            padding: 20px;
            margin: 50px auto;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        input {
            margin: 10px 0;
            padding: 10px;
            width: 100%;
            font-size: 14px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h2>Cadastro de Cliente</h2>
    <form action="CadastrarClienteServlet" method="post">
        <input type="text" name="nome" placeholder="Nome Completo" required>
        <input type="text" name="cpf" placeholder="CPF" required>
        <input type="email" name="email" placeholder="Email">
        <input type="text" name="celular" placeholder="Celular">
        <input type="date" name="dataNascimento" required>
        <button type="submit">Cadastrar</button>
    </form>
</body>
</html>

Tabela de Horários(tabelaHorarios.html):
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tabela de Horários</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }
        table {
            width: 80%;
            margin: 50px auto;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #007BFF;
            color: white;
        }
    </style>
</head>
<body>
    <h2>Horários Disponíveis</h2>
    <table>
        <thead>
            <tr>
                <th>Horário</th>
                <th>Barbeiro</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <!-- Dados dinâmicos -->
        </tbody>
    </table>
</body>
</html>


Tabela de Preços(tabelaprecos.html):
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tabela de Preços</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
        }
        table {
            width: 60%;
            margin: 50px auto;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
        }
        th {
            background-color: #007BFF;
            color: white;
        }
    </style>
</head>
<body>
    <h2>Tabela de Preços</h2>
    <table>
        <tr>
            <th>Serviço</th>
            <th>Preço</th>
        </tr>
        <tr>
            <td>Corte de Cabelo</td>
            <td>R$ 30,00</td>
        </tr>
        <tr>
            <td>Barba</td>
            <td>R$ 20,00</td>
        </tr>
        <tr>
            <td>Corte + Barba</td>
            <td>R$ 45,00</td>
        </tr>
    </table>
</body>
</html>


CRUD


1. Create (Criar)

Cadastro de Cliente:

<!-- cadastro.html -->
<form action="CadastrarClienteServlet" method="post">
    <input type="text" name="nome" placeholder="Nome Completo" required>
    <input type="text" name="cpf" placeholder="CPF" required>
    <input type="email" name="email" placeholder="Email">
    <input type="text" name="celular" placeholder="Celular">
    <input type="date" name="dataNascimento" required>
    <button type="submit">Cadastrar</button>
</form>

// CadastrarClienteServlet.java
@WebServlet("/CadastrarClienteServlet")
public class CadastrarClienteServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String nome = request.getParameter("nome");
        String cpf = request.getParameter("cpf");
        String email = request.getParameter("email");
        String celular = request.getParameter("celular");
        String dataNascimento = request.getParameter("dataNascimento");

        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASS)) {
            String query = "INSERT INTO clientes (nome, cpf, email, celular, data_nascimento) VALUES (?, ?, ?, ?, ?)";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setString(1, nome);
                stmt.setString(2, cpf);
                stmt.setString(3, email);
                stmt.setString(4, celular);
                stmt.setString(5, dataNascimento);
                stmt.executeUpdate();
                response.sendRedirect("login.html");
            }
        } catch (SQLException e) {
            e.printStackTrace();
            response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR, "Erro ao cadastrar cliente.");
        }
    }
}

2. Read (Ler)

Exibir Tabela de Horários:

<!-- tabelaHorarios.html -->
<table>
    <thead>
        <tr>
            <th>Horário</th>
            <th>Barbeiro</th>
            <th>Status</th>
        </tr>
    </thead>
    <tbody>
        <!-- Dados dinâmicos a partir do Servlet -->
    </tbody>
</table>

// ExibirHorariosServlet.java
@WebServlet("/ExibirHorariosServlet")
public class ExibirHorariosServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        List<Agendamento> agendamentos = new ArrayList<>();
        
        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASS)) {
            String query = "SELECT a.id, a.horario, a.status, c.nome as cliente, f.nome as barbeiro FROM agendamentos a " +
                           "JOIN clientes c ON a.cliente_id = c.id " +
                           "JOIN funcionarios f ON a.funcionario_id = f.id";
            try (PreparedStatement stmt = conn.prepareStatement(query);
                 ResultSet rs = stmt.executeQuery()) {
                while (rs.next()) {
                    Agendamento agendamento = new Agendamento();
                    agendamento.setId(rs.getInt("id"));
                    agendamento.setHorario(rs.getTimestamp("horario"));
                    agendamento.setStatus(rs.getString("status"));
                    agendamento.setCliente(rs.getString("cliente"));
                    agendamento.setBarbeiro(rs.getString("barbeiro"));
                    agendamentos.add(agendamento);
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        
        request.setAttribute("agendamentos", agendamentos);
        RequestDispatcher dispatcher = request.getRequestDispatcher("tabelaHorarios.html");
        dispatcher.forward(request, response);
    }
}

3. Update (Atualizar)

Alterar Status do Agendamento:

// AlterarStatusAgendamentoServlet.java
@WebServlet("/AlterarStatusAgendamentoServlet")
public class AlterarStatusAgendamentoServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int agendamentoId = Integer.parseInt(request.getParameter("agendamentoId"));
        String novoStatus = request.getParameter("status");

        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASS)) {
            String query = "UPDATE agendamentos SET status = ? WHERE id = ?";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setString(1, novoStatus);
                stmt.setInt(2, agendamentoId);
                stmt.executeUpdate();
                response.sendRedirect("exibirAgendamentos.html");
            }
        } catch (SQLException e) {
            e.printStackTrace();
            response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR, "Erro ao alterar status.");
        }
    }
}

4. Delete (Deletar)

Cancelar Agendamento:

// CancelarAgendamentoServlet.java
@WebServlet("/CancelarAgendamentoServlet")
public class CancelarAgendamentoServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int agendamentoId = Integer.parseInt(request.getParameter("agendamentoId"));

        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASS)) {
            String query = "UPDATE agendamentos SET status = 'Cancelado' WHERE id = ?";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setInt(1, agendamentoId);
                stmt.executeUpdate();
                response.sendRedirect("exibirAgendamentos.html");
            }
        } catch (SQLException e) {
            e.printStackTrace();
            response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR, "Erro ao cancelar agendamento.");
        }
    }
}

.
