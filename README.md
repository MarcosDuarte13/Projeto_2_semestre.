# Projeto_2_semestre.


Tela Login

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import javax.swing.JOptionPane;

public class Haaland extends javax.swing.JFrame {

    public Haaland() {
        initComponents();
    }

    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        lblUsuario = new javax.swing.JLabel();
        txtUsuario = new javax.swing.JTextField();
        lblSenha = new javax.swing.JLabel();
        txtSenha = new javax.swing.JPasswordField();
        btnEntrar = new javax.swing.JButton();
        jLabel1 = new javax.swing.JLabel();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        getContentPane().setLayout(null);

        lblUsuario.setFont(new java.awt.Font("Arial", 1, 10)); // NOI18N
        lblUsuario.setForeground(new java.awt.Color(51, 51, 51));
        lblUsuario.setText("Usuário");
        getContentPane().add(lblUsuario);
        lblUsuario.setBounds(260, 10, 70, 21);

        txtUsuario.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtUsuarioActionPerformed(evt);
            }
        });
        txtUsuario.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                txtUsuarioKeyPressed(evt);
            }
        });
        getContentPane().add(txtUsuario);
        txtUsuario.setBounds(230, 40, 100, 22);

        lblSenha.setFont(new java.awt.Font("Arial", 1, 10)); // NOI18N
        lblSenha.setForeground(new java.awt.Color(51, 51, 51));
        lblSenha.setText("Senha");
        getContentPane().add(lblSenha);
        lblSenha.setBounds(260, 70, 70, 13);

        txtSenha.setForeground(new java.awt.Color(204, 204, 204));
        txtSenha.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                txtSenhaKeyPressed(evt);
            }
        });
        getContentPane().add(txtSenha);
        txtSenha.setBounds(230, 90, 100, 20);

        btnEntrar.setFont(new java.awt.Font("Arial", 1, 10)); // NOI18N
        btnEntrar.setForeground(new java.awt.Color(204, 204, 204));
        btnEntrar.setText("Entrar");
        btnEntrar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnEntrarActionPerformed(evt);
            }
        });
        btnEntrar.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                btnEntrarKeyPressed(evt);
            }
        });
        getContentPane().add(btnEntrar);
        btnEntrar.setBounds(240, 120, 60, 20);

        jLabel1.setIcon(new javax.swing.ImageIcon(getClass().getResource("/logo.png"))); // NOI18N
        getContentPane().add(jLabel1);
        jLabel1.setBounds(0, -10, 333, 260);

        setSize(new java.awt.Dimension(351, 267));
        setLocationRelativeTo(null);
    }// </editor-fold>                        

    private void txtUsuarioKeyPressed(java.awt.event.KeyEvent evt) {                                      
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            txtSenha.requestFocus();
        }
    }                                     

    private void txtSenhaKeyPressed(java.awt.event.KeyEvent evt) {                                    
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            btnEntrar.requestFocus();
        }
    }                                   

    private void btnEntrarActionPerformed(java.awt.event.ActionEvent evt) {                                          
               try {
            //1 - Pegar o usuário e a senha digitados;
            String usuario, senha;
            usuario = txtUsuario.getText();
            senha = txtSenha.getText();
            //2 - Conectar no banco de dados haaland;
            Class.forName("com.mysql.cj.jdbc.Driver");
                   //3 - Buscar o usuário digitado na tabela usuario do banco de dados sistemabd;
                   try (Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin")) {
                       //3 - Buscar o usuário digitado na tabela usuario do banco de dados sistemabd;
                       PreparedStatement st = conectado.prepareStatement("SELECT * FROM usuarios WHERE usuario = ? AND senha = ?");
                       st.setString(1, usuario);
                       st.setString(2, senha);
                       ResultSet resultado = st.executeQuery();
                       //4 - Verificar se o usuário foi encontrado na tabela usuario do banco de dados.
                       if (resultado.next()) {
                           //Pega o nome e o cargo que veio na consulta ao banco de dados
                           String nome;
                           String cargo;
                           nome = resultado.getString("nome");
                           cargo = resultado.getString("cargo");
                           //Abrir o formulário Menu.java
                           Menu tela;
                           tela = new Menu(nome, cargo);
                           tela.setVisible(true);
                       } else {
                           JOptionPane.showMessageDialog(null, "Usuário e/ou senha inválidos");
                       }
                       //5 - Desconectar.
                   }
        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, "Driver não está na library");
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, "Você errou nos dados da conexão com o banco de dados");
        }

    }                                         

    private void btnEntrarKeyPressed(java.awt.event.KeyEvent evt) {                                     
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            btnEntrar.doClick();
        }
    }                                    

    private void txtUsuarioActionPerformed(java.awt.event.ActionEvent evt) {                                           


    }                                          

    public static void main(String args[]) {

        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(Haaland.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(Haaland.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(Haaland.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(Haaland.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
       
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new Haaland().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btnEntrar;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel lblSenha;
    private javax.swing.JLabel lblUsuario;
    private javax.swing.JPasswordField txtSenha;
    private javax.swing.JTextField txtUsuario;
    // End of variables declaration                   
}



Tela Menu

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.swing.JOptionPane;

public class Menu extends javax.swing.JFrame {
 //Construtor da classe Menu
    public Menu(String nome, String cargo) {
        initComponents();
        mnuAdmin.setVisible(false);
        lblSaudacao.setText("Bem vindo " + nome + " - Cargo: " + cargo);
        if (cargo.equalsIgnoreCase("gerente")) {
            mnuAdmin.setVisible(true);
        } else if (cargo.equalsIgnoreCase("estagiário")) {
            itmExcluirProdutos.setEnabled(false);
        }
    }
    
    public Menu() {
        initComponents();
    }

   
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        lblSaudacao = new javax.swing.JLabel();
        jLabel1 = new javax.swing.JLabel();
        jMenuBar1 = new javax.swing.JMenuBar();
        mnuProdutos = new javax.swing.JMenu();
        itmCadastrarProdutos = new javax.swing.JMenuItem();
        itmAlterarProdutos = new javax.swing.JMenuItem();
        itmExcluirProdutos = new javax.swing.JMenuItem();
        itmRelatoriosProdutos = new javax.swing.JMenuItem();
        jSeparator1 = new javax.swing.JPopupMenu.Separator();
        itmSair = new javax.swing.JMenuItem();
        mnuClientes = new javax.swing.JMenu();
        mnuAdmin = new javax.swing.JMenu();
        itmAlterarDadosUsuario = new javax.swing.JMenuItem();
        itmaExcluirUsuario = new javax.swing.JMenuItem();
        itmAdicionarUsuarios = new javax.swing.JMenuItem();
        itmExcluirTodosUsuarios = new javax.swing.JMenuItem();
        itmListarUsuarios = new javax.swing.JMenuItem();
        mnuAjuda = new javax.swing.JMenu();
        jSeparator2 = new javax.swing.JPopupMenu.Separator();

        getContentPane().setLayout(null);
        getContentPane().add(lblSaudacao);
        lblSaudacao.setBounds(190, 0, 600, 100);

        jLabel1.setIcon(new javax.swing.ImageIcon(getClass().getResource("/tala menu.png"))); // NOI18N
        getContentPane().add(jLabel1);
        jLabel1.setBounds(0, 0, 770, 420);

        mnuProdutos.setText("Produtos");

        itmCadastrarProdutos.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_C, java.awt.event.InputEvent.ALT_DOWN_MASK | java.awt.event.InputEvent.CTRL_DOWN_MASK));
        itmCadastrarProdutos.setText("Cadastrar");
        mnuProdutos.add(itmCadastrarProdutos);

        itmAlterarProdutos.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_L, java.awt.event.InputEvent.ALT_DOWN_MASK | java.awt.event.InputEvent.CTRL_DOWN_MASK));
        itmAlterarProdutos.setText("Alterar");
        itmAlterarProdutos.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmAlterarProdutosActionPerformed(evt);
            }
        });
        mnuProdutos.add(itmAlterarProdutos);

        itmExcluirProdutos.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_B, java.awt.event.InputEvent.ALT_DOWN_MASK | java.awt.event.InputEvent.CTRL_DOWN_MASK));
        itmExcluirProdutos.setText("Excluir");
        itmExcluirProdutos.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmExcluirProdutosActionPerformed(evt);
            }
        });
        mnuProdutos.add(itmExcluirProdutos);

        itmRelatoriosProdutos.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_R, java.awt.event.InputEvent.ALT_DOWN_MASK | java.awt.event.InputEvent.CTRL_DOWN_MASK));
        itmRelatoriosProdutos.setText("Relatórios");
        mnuProdutos.add(itmRelatoriosProdutos);
        mnuProdutos.add(jSeparator1);

        itmSair.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_S, java.awt.event.InputEvent.ALT_DOWN_MASK | java.awt.event.InputEvent.CTRL_DOWN_MASK));
        itmSair.setText("Sair");
        itmSair.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmSairActionPerformed(evt);
            }
        });
        mnuProdutos.add(itmSair);

        jMenuBar1.add(mnuProdutos);

        mnuClientes.setText("Clientes");
        jMenuBar1.add(mnuClientes);

        mnuAdmin.setText("Admin");

        itmAlterarDadosUsuario.setText("Alterar Dados do Usuário");
        itmAlterarDadosUsuario.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmAlterarDadosUsuarioActionPerformed(evt);
            }
        });
        mnuAdmin.add(itmAlterarDadosUsuario);

        itmaExcluirUsuario.setText("Excluir Usuário");
        itmaExcluirUsuario.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmaExcluirUsuarioActionPerformed(evt);
            }
        });
        mnuAdmin.add(itmaExcluirUsuario);

        itmAdicionarUsuarios.setText("Adicionar Usuário");
        itmAdicionarUsuarios.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmAdicionarUsuariosActionPerformed(evt);
            }
        });
        mnuAdmin.add(itmAdicionarUsuarios);

        itmExcluirTodosUsuarios.setText("Excluir Todos Usuários");
        mnuAdmin.add(itmExcluirTodosUsuarios);

        itmListarUsuarios.setText("Listar Usuários");
        itmListarUsuarios.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                itmListarUsuariosActionPerformed(evt);
            }
        });
        mnuAdmin.add(itmListarUsuarios);

        jMenuBar1.add(mnuAdmin);

        mnuAjuda.setText("Ajuda");
        mnuAjuda.add(jSeparator2);

        jMenuBar1.add(mnuAjuda);

        setJMenuBar(jMenuBar1);

        setSize(new java.awt.Dimension(649, 449));
        setLocationRelativeTo(null);
    }// </editor-fold>                        

    private void itmAlterarProdutosActionPerformed(java.awt.event.ActionEvent evt) {                                                   
        // TODO add your handling code here:
    }                                                  

    private void itmExcluirProdutosActionPerformed(java.awt.event.ActionEvent evt) {                                                   
        // TODO add your handling code here:
    }                                                  

    private void itmSairActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here:
    }                                       

    private void itmAlterarDadosUsuarioActionPerformed(java.awt.event.ActionEvent evt) {                                                       
        abrirTelaUsuario("Alterar");
    }                                                      

    private void itmaExcluirUsuarioActionPerformed(java.awt.event.ActionEvent evt) {                                                   

        abrirTelaUsuario("Excluir");
    }                                                  

    private void itmAdicionarUsuariosActionPerformed(java.awt.event.ActionEvent evt) {                                                     
        TelaUsuario tela;
        tela = new TelaUsuario();
        tela.setVisible(true);
    }                                                    

    private void itmListarUsuariosActionPerformed(java.awt.event.ActionEvent evt) {                                                  
        new ListaUsuario().setVisible(true);
    }                                                 

       private void abrirTelaUsuario(String operacao) {
        // 1 - Solicitar o usuário a ser alterado
        String u;
        u = JOptionPane.showInputDialog(null, "Digite o Usuario a " + operacao ,"Usuario", 1);
        if (u == null) {
            return;//stop
        }
        try {
            //2 - Conectar no banco de dados sistemabd;
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");
            //3 - Buscar o usuário digitado na tabela usuario do banco de dados haaland;
            PreparedStatement st = conectado.prepareStatement("SELECT * FROM usuarios WHERE usuario = ?");
            st.setString(1, u);
            ResultSet resultado = st.executeQuery();
            //4 - Verificar se o usuário foi encontrado na tabela usuario do banco de dados.
            if (resultado.next()) {
                //Pega o nome e o cargo que veio na consulta ao banco de dados
                String usuario, senha, nome, cargo;
                usuario = resultado.getString("usuario");
                senha = resultado.getString("senha");
                nome = resultado.getString("nome");
                cargo = resultado.getString("cargo");
                //4-Abrir o formulário Menu.java
                TelaUsuario tela;
                tela = new TelaUsuario(usuario, senha, nome, cargo, operacao);
                tela.setVisible(true);
            } else {
                JOptionPane.showMessageDialog(null, "Usuário não cadastrado");
            }
            //5 - Desconectar.
            conectado.close();
        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, "Driver não está na library");
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, "Você errou nos dados da conexão com o banco de dados");
        }

    }

    // Variables declaration - do not modify                     
    private javax.swing.JMenuItem itmAdicionarUsuarios;
    private javax.swing.JMenuItem itmAlterarDadosUsuario;
    private javax.swing.JMenuItem itmAlterarProdutos;
    private javax.swing.JMenuItem itmCadastrarProdutos;
    private javax.swing.JMenuItem itmExcluirProdutos;
    private javax.swing.JMenuItem itmExcluirTodosUsuarios;
    private javax.swing.JMenuItem itmListarUsuarios;
    private javax.swing.JMenuItem itmRelatoriosProdutos;
    private javax.swing.JMenuItem itmSair;
    private javax.swing.JMenuItem itmaExcluirUsuario;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JMenuBar jMenuBar1;
    private javax.swing.JPopupMenu.Separator jSeparator1;
    private javax.swing.JPopupMenu.Separator jSeparator2;
    private javax.swing.JLabel lblSaudacao;
    private javax.swing.JMenu mnuAdmin;
    private javax.swing.JMenu mnuAjuda;
    private javax.swing.JMenu mnuClientes;
    private javax.swing.JMenu mnuProdutos;
    // End of variables declaration                   

}

Tela Usuarios

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import javax.swing.JOptionPane;


public class TelaUsuario extends javax.swing.JFrame {

   
    public TelaUsuario() {
        initComponents();
          btnExcluir.setVisible(false);
        btnSalvarAlteracao.setVisible(false);
    }
  public TelaUsuario(String usuario, String senha, String nome, String cargo,String operacao) {
        initComponents();
        txtUsuario.setText(usuario);
        txtSenha.setText(senha);
        txtNome.setText(nome);
        cmbCargo.setSelectedItem(cargo);
        if(operacao.equals("excluir")){
        btnSalvar.setVisible(false);
        btnSalvarAlteracao.setVisible(false);
        }else if(operacao.equals("Alterar")){
        btnSalvar.setVisible(false);
        btnExcluir.setVisible(false);
        txtUsuario.setEnabled(false);
        }
    } 

 
    
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        lblNome = new javax.swing.JLabel();
        txtNome = new javax.swing.JTextField();
        txtUsuario = new javax.swing.JTextField();
        lblUsuario = new javax.swing.JLabel();
        lblSenha = new javax.swing.JLabel();
        txtSenha = new javax.swing.JTextField();
        cmbCargo = new javax.swing.JComboBox<>();
        lblCargo = new javax.swing.JLabel();
        btnSalvar = new javax.swing.JButton();
        btnExcluir = new javax.swing.JButton();
        btnSalvarAlteracao = new javax.swing.JButton();
        jLabel1 = new javax.swing.JLabel();

        getContentPane().setLayout(null);

        lblNome.setText("Nome");
        getContentPane().add(lblNome);
        lblNome.setBounds(10, 20, 90, 40);

        txtNome.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                txtNomeKeyPressed(evt);
            }
        });
        getContentPane().add(txtNome);
        txtNome.setBounds(70, 20, 160, 40);

        txtUsuario.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtUsuarioActionPerformed(evt);
            }
        });
        txtUsuario.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                txtUsuarioKeyPressed(evt);
            }
        });
        getContentPane().add(txtUsuario);
        txtUsuario.setBounds(70, 70, 160, 40);

        lblUsuario.setText("Usuário");
        getContentPane().add(lblUsuario);
        lblUsuario.setBounds(10, 70, 90, 40);

        lblSenha.setText("Senha");
        getContentPane().add(lblSenha);
        lblSenha.setBounds(10, 120, 90, 40);

        txtSenha.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtSenhaActionPerformed(evt);
            }
        });
        txtSenha.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                txtSenhaKeyPressed(evt);
            }
        });
        getContentPane().add(txtSenha);
        txtSenha.setBounds(70, 120, 160, 40);

        cmbCargo.setModel(new javax.swing.DefaultComboBoxModel<>(new String[] { " ", "Gerente", "Vendedor", "Farmacêutico", "Ver Todos" }));
        cmbCargo.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                cmbCargoActionPerformed(evt);
            }
        });
        cmbCargo.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                cmbCargoKeyPressed(evt);
            }
        });
        getContentPane().add(cmbCargo);
        cmbCargo.setBounds(70, 170, 160, 50);

        lblCargo.setText("Cargo");
        getContentPane().add(lblCargo);
        lblCargo.setBounds(10, 170, 90, 40);

        btnSalvar.setBackground(new java.awt.Color(204, 204, 204));
        btnSalvar.setForeground(new java.awt.Color(255, 255, 255));
        btnSalvar.setText("Salvar");
        btnSalvar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnSalvarActionPerformed(evt);
            }
        });
        btnSalvar.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                btnSalvarKeyPressed(evt);
            }
        });
        getContentPane().add(btnSalvar);
        btnSalvar.setBounds(10, 240, 140, 30);

        btnExcluir.setBackground(new java.awt.Color(204, 204, 204));
        btnExcluir.setForeground(new java.awt.Color(255, 255, 255));
        btnExcluir.setText("Excluir");
        btnExcluir.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnExcluirActionPerformed(evt);
            }
        });
        getContentPane().add(btnExcluir);
        btnExcluir.setBounds(80, 270, 140, 30);

        btnSalvarAlteracao.setBackground(new java.awt.Color(204, 204, 204));
        btnSalvarAlteracao.setForeground(new java.awt.Color(255, 255, 255));
        btnSalvarAlteracao.setText("Salvar Alteração");
        btnSalvarAlteracao.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnSalvarAlteracaoActionPerformed(evt);
            }
        });
        getContentPane().add(btnSalvarAlteracao);
        btnSalvarAlteracao.setBounds(150, 240, 140, 30);
        getContentPane().add(jLabel1);
        jLabel1.setBounds(-60, 10, 360, 320);

        setSize(new java.awt.Dimension(319, 341));
        setLocationRelativeTo(null);
    }// </editor-fold>                        

    private void txtNomeKeyPressed(java.awt.event.KeyEvent evt) {                                   
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            txtUsuario.requestFocus();
        }
    }                                  

    private void txtUsuarioActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
    }                                          

    private void txtUsuarioKeyPressed(java.awt.event.KeyEvent evt) {                                      
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            txtSenha.requestFocus();
        }
    }                                     

    private void txtSenhaActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void txtSenhaKeyPressed(java.awt.event.KeyEvent evt) {                                    
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            cmbCargo.requestFocus();
        }
    }                                   

    private void cmbCargoActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void cmbCargoKeyPressed(java.awt.event.KeyEvent evt) {                                    
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            btnSalvar.requestFocus();
        }
    }                                   

    private void btnSalvarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        //1 - Pegar as informações dos campos do formulário.
        String n, u, s, c;
        u = txtUsuario.getText();
        s = txtSenha.getText();
        n = txtNome.getText();
        c = cmbCargo.getSelectedItem().toString();
        //2 - Verificar se o campo txtUsuario do formulário, que é chave primária na tabela, não está vazio
        if (u.isEmpty()) { // se usuário está vazio
            JOptionPane.showMessageDialog(null, "É obrigatório digitar o usuário");
            txtUsuario.requestFocus();
            return; // stop
        }
        if (s.isEmpty()) { // se usuário está vazio
            JOptionPane.showMessageDialog(null, "É obrigatório digitar o usuário");
            txtUsuario.requestFocus();
            return; // stop
        }
        try {

            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");
            // 4- Inseriri os dados digitados na tabela do banco de dados
            PreparedStatement st = conectado.prepareStatement("INSERT INTO usuarios VALUES(?,?,?,?)");
            st.setString(1, u);
            st.setString(2, s);
            st.setString(3, n);
            st.setString(4, c);
            st.executeUpdate();
            //4.1
            JOptionPane.showMessageDialog(null, "Usuário cadastrado com sucesso");
            txtUsuario.setText("");
            txtNome.setText("");
            txtSenha.setText("");
            cmbCargo.setSelectedIndex(0);
            txtNome.requestFocus();

        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, "Driver não está na library");

        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, "Você errou nos dados da conexão com o banco de dados");
        }
    }                                         

    private void btnSalvarKeyPressed(java.awt.event.KeyEvent evt) {                                     
        if (evt.getKeyCode() == java.awt.event.KeyEvent.VK_ENTER) {
            btnSalvar.doClick();
        }
    }                                    

    private void btnExcluirActionPerformed(java.awt.event.ActionEvent evt) {                                           

        //1 - Perguntar se tem certeza que deseja excluir
        int resposta; // 0 - Sim; 1 - Não
        resposta = JOptionPane.showConfirmDialog(null, "Confirma?", "Confirmação", 0);
        //1.1 - Se a responta for sim
        if (resposta == 0) { //Resposta SIM
            //1.1.1 Obter o usuário no txtUsuario.
            String u = txtUsuario.getText();
            //1.1.2 - Conectar com o banco de dados.
            try {

                Class.forName("com.mysql.cj.jdbc.Driver");
                Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");
                //1.1.3 Excluir o usuario do banco de dados
                PreparedStatement st = conectado.prepareStatement("DELETE FROM usuarios WHERE usuario = ?");
                st.setString(1, u);
                st.executeUpdate(); //INSERT, UPDATE, DELETE
                //1.1.4 Mostrar a mensagem "Usuário excluído com sucesso" e limpar os campos.
                JOptionPane.showMessageDialog(null, "Usuário excluído com sucesso");
                //1.1.5 Fecha a TelaUsuario
                dispose();
                //1.1.6 Desconectar do banco de dados
                conectado.close();
            } catch (ClassNotFoundException | SQLException ex) {
                JOptionPane.showMessageDialog(null, "Mensagem de erro:" + ex.getMessage());
            }
            //1.2 - Se a resposta for não
            //1.2.2 Fecha a TelaUsuario
        } else {
            dispose();
        }
    }                                          

    private void btnSalvarAlteracaoActionPerformed(java.awt.event.ActionEvent evt) {                                                   
        //1 - Pegar as informações dos campos do formulário.
        String n, u, s, c;
        u = txtUsuario.getText();
        s = txtSenha.getText();
        n = txtNome.getText();
        c = cmbCargo.getSelectedItem().toString();
        //2 - Verificar se o campo txtUsuario do formulário, que é chave primária na tabela, não está vazio
        if (u.isEmpty()) { // se usuário está vazio
            JOptionPane.showMessageDialog(null, "É obrigatório digitar o usuário");
            txtUsuario.requestFocus();
            return; // stop
        }
        if (s.isEmpty()) { // se usuário está vazio
            JOptionPane.showMessageDialog(null, "É obrigatório digitar o usuário");
            txtUsuario.requestFocus();
            return; // stop
        }
        try {

            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");
            // 4- Inseriri os dados digitados na tabela do banco de dados
            PreparedStatement st = conectado.prepareStatement("UPDATE usuarios SET senha = ?, nome = ?, cargo = ? WHERE usuario = ?");
            st.setString(1, s);
            st.setString(2, n);
            st.setString(3, c);
            st.setString(4, u);
            st.executeUpdate();
            //4.1
            JOptionPane.showMessageDialog(null, "Usuário Alterado com sucesso");
            conectado.close();
            dispose();

        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, "Driver não está na library");

        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        }
    }                                                  

  
    // Variables declaration - do not modify                     
    private javax.swing.JButton btnExcluir;
    private javax.swing.JButton btnSalvar;
    private javax.swing.JButton btnSalvarAlteracao;
    private javax.swing.JComboBox<String> cmbCargo;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel lblCargo;
    private javax.swing.JLabel lblNome;
    private javax.swing.JLabel lblSenha;
    private javax.swing.JLabel lblUsuario;
    private javax.swing.JTextField txtNome;
    private javax.swing.JTextField txtSenha;
    private javax.swing.JTextField txtUsuario;
    // End of variables declaration                   
}


Lista Usuario


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;

public class ListaUsuario extends javax.swing.JFrame {
  
    public ListaUsuario() {
        initComponents();
        preencherTabela();
    }
  private void preencherTabela() {
        try {
            //1 - Conectar ao Banco de Dados
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");

            //2 - Buscar todos os usuários (SELECT)
            PreparedStatement st = conectado.prepareStatement("SELECT * FROM usuarios ORDER BY nome Asc");
            ResultSet resultado = st.executeQuery();
            //3 - Carregar os usuários na tabela tblUsuarios
            DefaultTableModel tblModelo;
            tblModelo = (DefaultTableModel) tblListaUsuarios.getModel();
            
            while (resultado.next()) {
                Object dados[] = {
                    resultado.getString("usuario"),
                    resultado.getString("senha"),
                    resultado.getString("nome"),
                    resultado.getString("cargo")
                };
                tblModelo.addRow(dados);

            }
            //4 - Desconectar do banco de dados
        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        }
    }
    
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jScrollPane1 = new javax.swing.JScrollPane();
        tblListaUsuarios = new javax.swing.JTable();
        lblCargo = new javax.swing.JLabel();
        cmbCargo = new javax.swing.JComboBox<>();

        getContentPane().setLayout(null);

        tblListaUsuarios.setModel(new javax.swing.table.DefaultTableModel(
            new Object [][] {

            },
            new String [] {
                "Usuário", "Senha", "Nome", "Cargo"
            }
        ) {
            boolean[] canEdit = new boolean [] {
                false, false, false, false
            };

            public boolean isCellEditable(int rowIndex, int columnIndex) {
                return canEdit [columnIndex];
            }
        });
        jScrollPane1.setViewportView(tblListaUsuarios);

        getContentPane().add(jScrollPane1);
        jScrollPane1.setBounds(0, 80, 640, 430);

        lblCargo.setText("Filtro");
        getContentPane().add(lblCargo);
        lblCargo.setBounds(10, 20, 27, 16);

        cmbCargo.setModel(new javax.swing.DefaultComboBoxModel<>(new String[] { " ", "Gerente", "Farmacêutico", "Vendedor", "Ver Todos" }));
        cmbCargo.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                cmbCargoActionPerformed(evt);
            }
        });
        getContentPane().add(cmbCargo);
        cmbCargo.setBounds(50, 10, 160, 50);

        setSize(new java.awt.Dimension(719, 542));
        setLocationRelativeTo(null);
    }// </editor-fold>                        

    private void cmbCargoActionPerformed(java.awt.event.ActionEvent evt) {                                         
        String c;
        c = cmbCargo.getSelectedItem().toString();
        if (c.equalsIgnoreCase("Ver Todos")) {
            preencherTabela();
            return; //stop
        }
        try {
            //1 - Conectar ao Banco de Dados
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conectado = DriverManager.getConnection("jdbc:mysql://localhost:3306/haaland", "root", "admin");

            //2 - Buscar os usuários pelo cargo (SELECT)
            PreparedStatement st = conectado.prepareStatement("SELECT * FROM usuarios WHERE cargo=?");
            st.setString(1, c);
            ResultSet resultado = st.executeQuery();
            //3 - Carregar os usuários na tabela tblUsuarios
            DefaultTableModel tblModelo;
            tblModelo = (DefaultTableModel) tblListaUsuarios.getModel();
            tblModelo.setRowCount(0);

            while (resultado.next()) {
                Object dados[] = {
                    resultado.getString("usuario"),
                    resultado.getString("senha"),
                    resultado.getString("nome"),
                    resultado.getString("cargo")
                };
                tblModelo.addRow(dados);

            }
            //4 - Desconectar do banco de dados
        } catch (ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        }
    }                                        

  
   
    // Variables declaration - do not modify                     
    private javax.swing.JComboBox<String> cmbCargo;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JLabel lblCargo;
    private javax.swing.JTable tblListaUsuarios;
    // End of variables declaration                   
}









