# Pi
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class TelaInicial extends JFrame {
    private JTextField nomeAdministradorField;
    private JPasswordField passwordField;
    private JButton entrarButton;
    private JButton sairButton;

    public TelaInicial() {
        initUI();
    }

    private void initUI() {
        setTitle("Memória Alegre - Login");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(800, 600); // Ajustei para um tamanho mais razoável
        setLocationRelativeTo(null);
        setResizable(false);

        // Carrega a imagem de fundo
        ImageIcon backgroundIcon = new ImageIcon("**c:/Users/25.00961-4/Downloads/image0.jpeg**");
        Image backgroundImage = backgroundIcon.getImage();

        // Painel principal com imagem de fundo
        BackgroundPanel mainPanel = new BackgroundPanel(backgroundImage);
        mainPanel.setLayout(new GridBagLayout());
        mainPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));

        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        // Título
        JLabel tituloLabel = new JLabel("Acesso Administrativo");
        tituloLabel.setFont(new Font("Trebuchet MS", Font.BOLD, 36));
        tituloLabel.setHorizontalAlignment(SwingConstants.CENTER);
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.gridwidth = 2;
        mainPanel.add(tituloLabel, gbc);

        // Campo Nome Administrador
        JLabel nomeLabel = new JLabel("Nome Administrador:");
        nomeLabel.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridy = 1;
        gbc.gridwidth = 1;
        mainPanel.add(nomeLabel, gbc);

        nomeAdministradorField = new JTextField(20);
        nomeAdministradorField.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridx = 1;
        mainPanel.add(nomeAdministradorField, gbc);

        // Campo Senha
        JLabel senhaLabel = new JLabel("Senha:");
        senhaLabel.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridx = 0;
        gbc.gridy = 2;
        mainPanel.add(senhaLabel, gbc);

        passwordField = new JPasswordField(20);
        passwordField.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridx = 1;
        mainPanel.add(passwordField, gbc);

        // Painel de botões
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 20, 10));
        buttonPanel.setOpaque(false);

        entrarButton = new JButton("Entrar");
        entrarButton.setFont(new Font("Trebuchet MS", Font.BOLD, 14));
        entrarButton.addActionListener(this::entrarAction);
        buttonPanel.add(entrarButton);

        sairButton = new JButton("Sair");
        sairButton.setFont(new Font("Trebuchet MS", Font.BOLD, 14));
        sairButton.addActionListener(this::sairAction);
        buttonPanel.add(sairButton);

        gbc.gridx = 0;
        gbc.gridy = 3;
        gbc.gridwidth = 2;
        mainPanel.add(buttonPanel, gbc);

        add(mainPanel);
    }

    private void entrarAction(ActionEvent evt) {
        String nome = nomeAdministradorField.getText();
        String senha = new String(passwordField.getPassword());

        if ("admin@email.com".equals(nome) && "admin".equals(senha)) {
            JOptionPane.showMessageDialog(this, "Login bem-sucedido!");
            this.dispose();
        } else {
            JOptionPane.showMessageDialog(this,
                "Credenciais inválidas!",
                "Erro de Login",
                JOptionPane.ERROR_MESSAGE);
        }
    }

    private void sairAction(ActionEvent evt) {
        int confirm = JOptionPane.showConfirmDialog(
            this,
            "Deseja realmente sair?",
            "Sair",
            JOptionPane.YES_NO_OPTION);
           
        if (confirm == JOptionPane.YES_OPTION) {
            System.exit(0);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            try {
                UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
            } catch (Exception ex) {
                ex.printStackTrace();
            }

            TelaInicial tela = new TelaInicial();
            tela.setVisible(true);
        });
    }

    // Painel personalizado para imagem de fundo
    class BackgroundPanel extends JPanel {
        private Image backgroundImage;

        public BackgroundPanel(Image backgroundImage) {
            this.backgroundImage = backgroundImage;
        }

        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
        }
    }
}
