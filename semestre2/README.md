### Sistema de Gerenciamento de Vagas - Dom Rock
2° Semestre - 02/2022

Parceiro Acadêmico: Pro4Tech
<p align="center"><img src="./pro4tech-logo.png" widht="20%"></img>

---

## Empresa parceira

A Pro4tech é uma empresa que visa a transformação digital como um de seus pilares. Seu produto está voltado para criação de soluções digitais, ágeis e inovadoras por meio do desenvolvimento de pessoas. A empresa possui seu portifólio de serviços voltados para soluções em Aplicações Transacionais (Web/App), Aplicações Analíticas (BI/Analytics), Redesenho de Processos de Negócio, Inteligência Artificial (IA), Robotização de Processos (RPA) e Internet das Coisas (IoT).

---

## 💻 Nossa proposta

A Pro4tech está abrindo varias vagas para contratação de novos funcionários, com isso sentiu a necessidade de ter um software onde pudesse registrar e ter todo o controle das vagas que estão ofertando no mercado.

## Solução para o problema
A solução para essa demanda será a criação de um sistema desktop onde será possível cadastrar vagas, excluir vagas, editar vagas, cadastrar usuários, aplicação da vaga pelo usuário e extrair relatórios.

---

## Lições Aprendidas

### **Hard Skills**

Durante o desenvolvimento do projeto, pude aprimorar diversas habilidades técnicas essenciais para o desenvolvimento de uma assistente virtual. Aqui estão as principais **hard skills** que adquiri:

- **Desenvolvimento de Interface Gráfica**: Aprendi a criar interfaces gráficas de usuário utilizando **Java Swing**.
  
- **Conexão com Banco de Dados**: Adquiri conhecimentos sobre a **conexão e manipulação de dados** em um banco de dados **MySQL** utilizando a API **JDBC**, o que permitiu integrar o sistema com um banco de dados relacional para armazenar informações de usuários.
  
- **Implementação de Funcionalidades**: Desenvolvi habilidades em implementar funcionalidades como login, cadastro de usuários e autenticação, fundamentais para garantir a segurança e a interação no sistema.

---

### **Soft Skills**

Além das habilidades técnicas, também trabalhei no desenvolvimento de habilidades interpessoais essenciais para o sucesso em um projeto colaborativo. Aqui estão as principais **soft skills** que desenvolvi durante o projeto:

- **Flexibilidade e Adaptabilidade**: Aprendi a adaptar rapidamente os planos e as abordagens do projeto frente a mudanças de requisitos ou desafios inesperados, garantindo a continuidade do desenvolvimento sem comprometer a qualidade.
- **Empatia e Escuta Ativa**: Tive a oportunidade de ouvir as necessidades dos membros da equipe e utilizá-las para tomar decisões mais assertivas, ajudando a criar um ambiente de trabalho mais harmonioso e colaborativo.
- **Liderança e Proatividade**: Assumi uma postura mais proativa, tomando a frente em algumas tarefas e ajudando a coordenar a equipe para garantir que as entregas fossem feitas dentro dos prazos estipulados.
- **Gestão de Conflitos**: Trabalhei na resolução de divergências de opinião e sugestões dentro da equipe, garantindo que as discussões fossem construtivas e que todos os pontos de vista fossem respeitados.
  
---

## Contribuições Individuais
<details>
  <summary><b>ClassesConexao: Acesso a Banco de Dados</b></summary>
  <br>
  <p>O código abaixo implementa a classe `vagasDAO`, responsável por interagir com o banco de dados para recuperar informações sobre vagas e candidatos. Aqui está uma explicação detalhada do que acontece no código:</p>
  
```java
package ClassesConexao;

import java.sql.Connection;
import java.sql.Date;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;
import java.sql.DriverManager;

import javax.swing.JOptionPane;

public class vagasDAO {
    private Connection con;
    private String carga_horaria;

    public String getCarga_horaria() {
        return carga_horaria;
    }

    public void setCarga_horaria(String carga_horaria) {
        this.carga_horaria = carga_horaria;
    }

    ResultSet rs;
    PreparedStatement ps;
    // Conexão com o banco de dados
    String url = "jdbc:mysql://localhost/pro4tech";
    String user = "root";
    String password = "39339533";

    // Método para recuperar as vagas disponíveis no banco de dados
    public ArrayList<String> vagas() {
        ArrayList<String> vg = new ArrayList<String>();
        System.out.println("teste");

        try {
            // Estabelece a conexão com o banco de dados
            con = DriverManager.getConnection(url, user, password);
            // Prepara a consulta SQL para recuperar os nomes das vagas
            ps = con.prepareStatement("SELECT nome_vaga FROM Vagas");
            // Executa a consulta SQL
            ResultSet rs = ps.executeQuery();
            // Percorre o resultado da consulta e adiciona os nomes das vagas à lista
            while (rs.next()) {
                vg.add(rs.getString("nome_vaga"));
            }
            // Fecha o ResultSet, PreparedStatement e a conexão com o banco de dados
            rs.close();
            ps.close();
            con.close();
        } catch (Exception e) {
            // Exibe uma mensagem de erro em caso de falha na recuperação das vagas
            JOptionPane.showMessageDialog(null, "Ocorreu erro ao carregar a Combo Box", "Erro",
                    JOptionPane.ERROR_MESSAGE);
        }
        return vg;
    }

    // Método para recuperar os candidatos de uma vaga específica no banco de dados
    public ArrayList<String> candidato() {
        ArrayList<String> candidato = new ArrayList<String>();

        try {
            // Estabelece a conexão com o banco de dados
            con = DriverManager.getConnection(url, user, password);
            // Prepara a consulta SQL para recuperar os CPFs dos candidatos de uma vaga específica
            ps = con.prepareStatement("SELECT * from candidato_vaga where nome_vaga = '"
                    + Singleton.getInstance().nomeVaga + "'");
            // Executa a consulta SQL
            ResultSet rs = ps.executeQuery();
            // Percorre o resultado da consulta e adiciona os CPFs dos candidatos à lista
            while (rs.next()) {
                candidato.add(rs.getString("cpf"));
            }
            // Fecha o ResultSet, PreparedStatement e a conexão com o banco de dados
            rs.close();
            ps.close();
            con.close();
        } catch (Exception e) {
            // Exibe uma mensagem de erro em caso de falha na recuperação dos candidatos
            JOptionPane.showMessageDialog(null, "Ocorreu erro ao carregar a Combo Box", "Erro",
                    JOptionPane.ERROR_MESSAGE);
        }
        return candidato;
    }
}
```
  <p>A classe `vagasDAO` possui dois métodos principais: `vagas()` e `candidato()`. O primeiro método é responsável por recuperar os nomes das vagas disponíveis no banco de dados, enquanto o segundo método recupera os CPFs dos candidatos de uma vaga específica.</p>
  </details>
 
<details>
  <summary><b>TelaLogin: Interface de Login</b></summary>
  <br>
  <p>O código abaixo implementa a classe `TelaLogin`, que representa a interface de login do sistema. Aqui está uma explicação detalhada do que acontece no código:</p>
  
```java
package ClassesConexao;

import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import java.awt.Font;
import javax.swing.JTextField;
import javax.swing.JPasswordField;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.awt.event.ActionEvent;
import java.awt.Color;
import javax.swing.SwingConstants;
import javax.swing.ImageIcon;

public class TelaLogin extends JFrame {

    private static final long serialVersionUID = 1L;
    private JPanel contentPane;
    private JTextField tfUsuario;
    private JPasswordField pfSenha;
    private JButton btnCadastrar;
    private JButton btnEntrar;
    private JLabel lblAquiTemUma;
    private JLabel lblOlSejaBemvindo;
    private JLabel lblFaaSeuLogin_1;
    private JLabel lblNewLabel_1;

    public static void main(String[] args) {
        EventQueue.invokeLater(new Runnable() {
            public void run() {
                try {
                    TelaLogin frame = new TelaLogin();
                    frame.setVisible(true);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public TelaLogin() {
        btnEntrar = new JButton("ENTRAR");
        btnEntrar.setBackground(new Color(255, 140, 0));
        btnEntrar.setForeground(Color.BLACK);
        btnEntrar.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    Connection con = Conexao.faz_conexao();
                    String sql = "select *from cadastro_usuario where email=? and senha= ?";
                    PreparedStatement stmt = con.prepareStatement(sql);
                    stmt.setString(1, tfUsuario.getText());
                    stmt.setString(2, new String(pfSenha.getPassword()));
                    ResultSet rs = stmt.executeQuery();
                    if (rs.next()) {
                        JOptionPane.showMessageDialog(null, "Entrando!");
                        Singleton.getInstance().nomeUsuario = rs.getString("nome");
                        Singleton.getInstance().cpfUsuario = rs.getString("cpf");
                        System.out.println(Singleton.getInstance().nomeUsuario);
                        TelaOpcoes exibir = new TelaOpcoes();
                        exibir.setVisible(true);
                        setVisible(false);
                    } else {
                        try {
                            String sql1 = "select * from cadastro_funcionario where email=? and senha= ?";
                            PreparedStatement stmt1 = con.prepareStatement(sql1);
                            stmt1.setString(1, tfUsuario.getText());
                            stmt1.setString(2, new String(pfSenha.getPassword()));
                            ResultSet rs1 = stmt1.executeQuery();
                            if (rs1.next()) {
                                JOptionPane.showMessageDialog(null, "Entrando!");
                                Singleton.getInstance().nomeFuncionario = rs1.getString("nome");
                                TelaOpcoesFuncionario exibir = new TelaOpcoesFuncionario();
                                exibir.setVisible(true);
                                setVisible(false);
                            } else {
                                try {
                                    String sql2 = "select * from cadastro_admin where email = ? and senha= ?";
                                    PreparedStatement stmt2 = con.prepareStatement(sql2);
                                    stmt2.setString(1, tfUsuario.getText());
                                    stmt2.setString(2, new String(pfSenha.getPassword()));
                                    ResultSet rs2 = stmt2.executeQuery();
                                    if (rs2.next()) {
                                        JOptionPane.showMessageDialog(null, "Entrando!");
                                        Singleton.getInstance().nomeFuncionario = "vitoria";
                                        TelaMenuRH exibir = new TelaMenuRH();
                                        exibir.setVisible(true);
                                        setVisible(false);
                                    } else {
                                        message.setText("E-mail ou senha incorreta!!");
                                    }
                                    stmt2.close();
                                    con.close();
                                } catch (Exception e2) {
                                    e2.printStackTrace();
                                }
                            }
                            stmt1.close();
                            con.close();
                        } catch (SQLException e1) {
                            e1.printStackTrace();
                        }
                    }
                    stmt.close();
                    con.close();
                } catch (SQLException e1) {
                    e1.printStackTrace();
                }
            }
        });

```
  <p>A classe `TelaLogin` representa a tela de login do sistema. Ela possui campos para inserção do e-mail e senha do usuário, botões para entrar e cadastrar, além de mensagens de erro e informações para orientar o usuário.</p>
</details>

---


## Contribuições Coletivas
### Tela de visualização de currículo do usuário
<details> <summary><b>Clique para ver o código e explicação</b></summary>

Essa tela foi criada para exibir e gerenciar as informações de um currículo de um candidato. Ela permite visualizar detalhes sobre o candidato, como quem ele é, sua formação acadêmica e sua experiência profissional. Aqui está uma explicação simples das contribuições feitas para o desenvolvimento dessa interface:

- Conexão com o Banco de Dados: A tela se conecta ao banco de dados usando JDBC para recuperar informações sobre o candidato e exibi-las em campos de texto, como "Quem Sou Eu" e "Formação".

- Feedback e Avaliação: A tela permite ao responsável pela avaliação do candidato registrar seu feedback, selecionando uma opção de uma lista suspensa, e pode marcar o candidato como "Aprovado" ou "Reprovado" clicando nos botões correspondentes. Essas ações são registradas no banco de dados.

- Ações de Botões: Dois botões principais, "APROVADO" e "REPROVADO", estão disponíveis para que o responsável pela avaliação selecione o status do candidato. Quando clicados, os dados são salvos no banco de dados com a avaliação.

```java
package ClassesConexao;

import java.awt.EventQueue;

import javax.swing.DropMode;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.table.DefaultTableModel;
import java.awt.Font;
import java.sql.Connection;
import java.sql.Date;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.awt.Color;
import javax.swing.event.AncestorListener;
import javax.swing.event.AncestorEvent;
import javax.swing.SwingConstants;
import javax.swing.DefaultComboBoxModel;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.border.BevelBorder;
import java.awt.event.ActionEvent;
import javax.swing.border.BevelBorder;
import javax.swing.border.BevelBorder;


public class TelaVisualizacaoCurriculo extends JFrame {

	private JPanel contentPane;
	private JTextField tfQuemSouEu;
	private JTextField tfFormacao;
	private JTextField tfFeedback;
	private JTextField tfExperiencia;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					TelaVisualizacaoCurriculo frame = new TelaVisualizacaoCurriculo();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public TelaVisualizacaoCurriculo() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 1920, 1080);
		contentPane = new JPanel();
		contentPane.setForeground(Color.BLACK);
		contentPane.setBackground(Color.WHITE);
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setExtendedState(MAXIMIZED_BOTH);

		setContentPane(contentPane);
		contentPane.setLayout(null);
		JLabel lblNewLabel = new JLabel("");
		lblNewLabel.setIcon(new ImageIcon("C:\\Users\\Ariane Sousa\\Desktop\\PROJETOS\\Pro4Tech\\icons\\iconPro4Tech.jpg"));
		lblNewLabel.setBounds(0, 0, 500, 109);
		contentPane.add(lblNewLabel);
		
		JLabel lblNewLabel_1 = new JLabel("VISUALIZAÇÃO CURRÍCULO");
		lblNewLabel_1.setForeground(Color.BLACK);
		lblNewLabel_1.setFont(new Font("Arial", Font.BOLD, 20));
		lblNewLabel_1.setBounds(79, 129, 275, 33);
		contentPane.add(lblNewLabel_1);
		
		JLabel lblNewLabel_2 = new JLabel("QUEM SOU EU?");
		lblNewLabel_2.setForeground(Color.BLACK);
		lblNewLabel_2.setFont(new Font("Arial", Font.PLAIN, 18));
		lblNewLabel_2.setBounds(79, 172, 157, 22);
		contentPane.add(lblNewLabel_2);
		
		tfQuemSouEu = new JTextField();
		tfQuemSouEu.setDisabledTextColor(Color.BLACK);
		tfQuemSouEu.setCaretColor(Color.BLACK);
		tfQuemSouEu.setHorizontalAlignment(SwingConstants.LEFT);
		tfQuemSouEu.setForeground(Color.BLACK);
		tfQuemSouEu.addAncestorListener(new AncestorListener() {
			public void ancestorAdded(AncestorEvent event) {
				
				try {
					Connection con = Conexao.faz_conexao();
					String sql = "select * from cadastro_usuario where nome = '" + Singleton.getInstance().Candidato + "'";
					PreparedStatement stmt = con.prepareStatement(sql);
					ResultSet rs = stmt.executeQuery();
					while(rs.next()) {
						tfQuemSouEu.setText(rs.getString("quem_sou_eu"));
					}
				} catch (Exception e) {
					// TODO: handle exception
				}
				
			}
			public void ancestorMoved(AncestorEvent event) {
			}
			public void ancestorRemoved(AncestorEvent event) {
			}
		});
		tfQuemSouEu.setEnabled(false);
		tfQuemSouEu.setEditable(false);
		tfQuemSouEu.setColumns(10);
		tfQuemSouEu.setToolTipText("Sobre você!");
		tfQuemSouEu.setFont(new Font("Arial", Font.PLAIN, 20));
		tfQuemSouEu.setBounds(79, 204, 639, 98);
		contentPane.add(tfQuemSouEu);
		
		JLabel lblNewLabel_3 = new JLabel("FORMAÇÃO");
		lblNewLabel_3.setForeground(Color.BLACK);
		lblNewLabel_3.setFont(new Font("Arial", Font.PLAIN, 18));
		lblNewLabel_3.setBounds(843, 172, 121, 22);
		contentPane.add(lblNewLabel_3);
		
		tfFormacao = new JTextField();
		tfFormacao.setDisabledTextColor(Color.BLACK);
		tfFormacao.setCaretColor(Color.BLACK);
		tfFormacao.setForeground(Color.BLACK);
		tfFormacao.addAncestorListener(new AncestorListener() {
			public void ancestorAdded(AncestorEvent event) {
				try {
					Connection con = Conexao.faz_conexao();
					String sql = "select * from cadastro_usuario where nome = '" + Singleton.getInstance().Candidato + "'";
					PreparedStatement stmt = con.prepareStatement(sql);
					ResultSet rs = stmt.executeQuery();
					while(rs.next()) {
						tfFormacao.setText(rs.getString("formaçao_acad"));
					}
				} catch (Exception e) {
					// TODO: handle exception
				}
			}
			public void ancestorMoved(AncestorEvent event) {
			}
			public void ancestorRemoved(AncestorEvent event) {
			}
		});
		tfFormacao.setEnabled(false);
		tfFormacao.setEditable(false);
		tfFormacao.setFont(new Font("Arial", Font.PLAIN, 18));
		tfFormacao.setToolTipText("Formação da mais recente até a mais antiga!");
		tfFormacao.setBounds(843, 206, 622, 96);
		contentPane.add(tfFormacao);
		tfFormacao.setColumns(10);
		
		JLabel lblNewLabel_4 = new JLabel("EXPERIÊNCIA PROFISSIONAL");
		lblNewLabel_4.setForeground(Color.BLACK);
		lblNewLabel_4.setFont(new Font("Arial", Font.PLAIN, 18));
		lblNewLabel_4.setBounds(79, 336, 262, 40);
		contentPane.add(lblNewLabel_4);
		
		JComboBox cbxFeedBack = new JComboBox();
		cbxFeedBack.setModel(new DefaultComboBoxModel(new String[] {"Tempo de experiência insuficiente", "Formação irrelevante ", "Perfil inadequado", "Modelo de trabalho incoerente com o desejado", "Salário incompatível"}));
		cbxFeedBack.setForeground(Color.BLACK);
		cbxFeedBack.setToolTipText("Feedback breve");
		cbxFeedBack.setMaximumRowCount(10);
		cbxFeedBack.setFont(new Font("Arial", Font.PLAIN, 18));
		cbxFeedBack.setBounds(79, 679, 867, 40);
		contentPane.add(cbxFeedBack);
		
		JButton btnNewButton_APROVADO = new JButton("APROVADO");
		btnNewButton_APROVADO.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				
				try {
					
					Connection con = Conexao.faz_conexao();
					String sql = "select * from cadastro_usuario where nome = '" + Singleton.getInstance().Candidato + "'";
					PreparedStatement stmt = con.prepareStatement(sql);
					ResultSet rs = stmt.executeQuery();
					while(rs.next()) {
						Singleton.getInstance().CandidatoCPF = rs.getString("cpf");
						Connection con1 = Conexao.faz_conexao();
						String sql1 = "select * from cadastro_funcionario where nome = '" + Singleton.getInstance().nomeFuncionario + "'";
						PreparedStatement stmt1 = con1.prepareStatement(sql1);
						ResultSet rs1 = stmt1.executeQuery();
						while(rs1.next()) {
							Singleton.getInstance().FuncionarioEMAIL = rs1.getString("email");
						}
						stmt1.close();
						con1.close();
					}
					stmt.close();
					con.close();
				} catch (SQLException e1) {
					e1.printStackTrace();
					JOptionPane.showMessageDialog(null, "ERRO!");
				} 
				
				try {
					Connection con = Conexao.faz_conexao();
					String sql = "insert into inscricao(nome_vaga, avaliacao, status_vaga, feedback_geral, feedback_pontual, cpf, email) values (?, ?, ?, ?, ?, ?, ?)";
					PreparedStatement stmt = con.prepareStatement(sql);
					
					stmt.setString(1, Singleton.getInstance().nomeVaga);
					stmt.setString(2, "APROVADO");
					stmt.setString(3, "ABERTA");
					stmt.setString(4, tfFeedback.getText());
					stmt.setString(5, "-");
					stmt.setString(6, Singleton.getInstance().CandidatoCPF);
					stmt.setString(7, Singleton.getInstance().FuncionarioEMAIL);
					
					stmt.execute();
					stmt.close();
					con.close();
					JOptionPane.showMessageDialog(null, "Avaliação realizada");
				} catch (Exception e2) {
					JOptionPane.showMessageDialog(null, "Faltando informações obrigatórias!!");
				}
				
			}
		});
		btnNewButton_APROVADO.setForeground(Color.BLACK);
		btnNewButton_APROVADO.setBackground(new Color(241, 133, 36));
		btnNewButton_APROVADO.setFont(new Font("Arial", Font.PLAIN, 18));
		btnNewButton_APROVADO.setBounds(1140, 421, 156, 52);
		contentPane.add(btnNewButton_APROVADO);
		
		JButton btnReprovado = new JButton("REPROVADO");
		btnReprovado.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					
					Connection con = Conexao.faz_conexao();
					String sql = "select * from cadastro_usuario where nome = '" + Singleton.getInstance().Candidato + "'";
					PreparedStatement stmt = con.prepareStatement(sql);
					ResultSet rs = stmt.executeQuery();
					while(rs.next()) {
						Singleton.getInstance().CandidatoCPF = rs.getString("cpf");
						Connection con1 = Conexao.faz_conexao();
						String sql1 = "select * from cadastro_funcionario where nome = '" + Singleton.getInstance().nomeFuncionario + "'";
						PreparedStatement stmt1 = con1.prepareStatement(sql1);
						ResultSet rs1 = stmt1.executeQuery();
						while(rs1.next()) {
							Singleton.getInstance().FuncionarioEMAIL = rs1.getString("email");
						}
						stmt1.close();
						con1.close();
					}
					stmt.close();
					con.close();
					
				} catch (SQLException e1) {
					e1.printStackTrace();
					JOptionPane.showMessageDialog(null, "ERRO!");
				} 
				
				try {
					Connection con = Conexao.faz_conexao();
					String sql = "insert into inscricao(nome_vaga, avaliacao, status_vaga, feedback_geral, feedback_pontual, cpf, email) values (?, ?, ?, ?, ?, ?, ?)";
					PreparedStatement stmt = con.prepareStatement(sql);
					
					stmt.setString(1, Singleton.getInstance().nomeVaga);
					stmt.setString(2, "REPROVADO");
					stmt.setString(3, "ABERTA");
					stmt.setString(4, tfFeedback.getText());
					stmt.setString(5, cbxFeedBack.getToolTipText());
					stmt.setString(6, Singleton.getInstance().CandidatoCPF);
					stmt.setString(7, Singleton.getInstance().FuncionarioEMAIL);
					
					stmt.execute();
					stmt.close();
					con.close();
					JOptionPane.showMessageDialog(null, "Avaliação realizada!");
				} catch (Exception e2) {
					JOptionPane.showMessageDialog(null, "Faltando informações obrigatórias!!");
				}
			}
		});
		btnReprovado.setForeground(Color.BLACK);
		btnReprovado.setFont(new Font("Arial", Font.PLAIN, 18));
		btnReprovado.setBackground(new Color(241, 133, 36));
		btnReprovado.setBounds(1140, 528, 156, 52);
		contentPane.add(btnReprovado);
		
		JLabel lblNewLabel_9 = new JLabel("FEEDBACK GERAL:");
		lblNewLabel_9.setForeground(Color.BLACK);
		lblNewLabel_9.setFont(new Font("Arial", Font.PLAIN, 18));
		lblNewLabel_9.setBounds(79, 483, 191, 40);
		contentPane.add(lblNewLabel_9);
		
		tfFeedback = new JTextField();
		tfFeedback.setCaretColor(Color.BLACK);
		tfFeedback.setHorizontalAlignment(SwingConstants.LEFT);
		tfFeedback.setForeground(Color.BLACK);
		tfFeedback.setFont(new Font("Arial", Font.PLAIN, 18));
		tfFeedback.setBounds(79, 528, 867, 85);
		contentPane.add(tfFeedback);
		tfFeedback.setColumns(10);
		
		JLabel lblNewLabel_10 = new JLabel("FEEDBACK PONTUAL:");
		lblNewLabel_10.setForeground(Color.BLACK);
		lblNewLabel_10.setFont(new Font("Arial", Font.PLAIN, 18));
		lblNewLabel_10.setBounds(79, 647, 206, 22);
		contentPane.add(lblNewLabel_10);
		
		tfExperiencia = new JTextField();
		tfExperiencia.setDisabledTextColor(Color.BLACK);
		tfExperiencia.setCaretColor(Color.BLACK);
		tfExperiencia.setHorizontalAlignment(SwingConstants.LEFT);
		tfExperiencia.setForeground(Color.BLACK);
		tfExperiencia.addAncestorListener(new AncestorListener() {
			public void ancestorAdded(AncestorEvent event) {
				try {
					Connection con = Conexao.faz_conexao();
					String sql = "select * from cadastro_usuario where nome = '" + Singleton.getInstance().Candidato + "'";
					PreparedStatement stmt = con.prepareStatement(sql);
					ResultSet rs = stmt.executeQuery();
					while(rs.next()) {
						tfExperiencia.setText(rs.getString("experiencia_profissional"));
					}
				} catch (Exception e) {
					// TODO: handle exception
				}
			}
			public void ancestorMoved(AncestorEvent event) {
			}
			public void ancestorRemoved(AncestorEvent event) {
			}
		});
		tfExperiencia.setToolTipText("Sobre você!");
		tfExperiencia.setFont(new Font("Arial", Font.PLAIN, 20));
		tfExperiencia.setEnabled(false);
		tfExperiencia.setEditable(false);
		tfExperiencia.setColumns(10);
		tfExperiencia.setBounds(79, 375, 639, 98);
		contentPane.add(tfExperiencia);
		
		JLabel lblNewLabel_5 = new JLabel("");
		lblNewLabel_5.setBounds(208, 10, 553, 90);

		contentPane.add(lblNewLabel_5);

		contentPane.add(lblNewLabel_5);
		
		JButton voltar = new JButton("VOLTAR");
		voltar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				if(Singleton.getInstance().nomeFuncionario  == "vitoria") {
					TelaMenuRH exibir = new TelaMenuRH();
					exibir.setVisible(true);
					setVisible(false);
				} else {
					TelaOpcoesFuncionario exibir = new TelaOpcoesFuncionario();
					exibir.setVisible(true);
					setVisible(false);
				}
			}
		});
		voltar.setForeground(Color.BLACK);
		voltar.setFont(new Font("Arial", Font.PLAIN, 18));
		voltar.setBackground(new Color(241, 133, 36));
		voltar.setBounds(10, 729, 156, 52);
		contentPane.add(voltar);
	}
}
```
</details>

---

## Tecnologias Utilizadas

- **Java**: Linguagem de programação utilizada para o desenvolvimento do sistema.
  
- **Java Swing**: Biblioteca gráfica utilizada para criar a interface de usuário.
  
- **JDBC (Java Database Connectivity)**: API do Java para conexão e interação com bancos de dados relacionais.
  
- **MySQL**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar informações sobre usuários e autenticação.
  
- **Figma**: Utilizado para o desenvolvimento e prototipação das wireframes.
  
---


## Conclusão

Ao trabalhar na integração de uma aplicação com uma base de dados, utilizando Java para a interface e o código, pude perceber a importância desse conhecimento para o desenvolvimento de sistemas mais eficientes e dinâmicos. A conexão com a base de dados me permitiu otimizar operações de leitura e escrita, garantindo uma interação fluída com os dados. Esse aprendizado me ajudou a melhorar a gestão de grandes volumes de informações e contribuiu para tornar a aplicação mais escalável e fácil de manter, resultando em soluções mais robustas e adaptáveis às necessidades dos usuários.
