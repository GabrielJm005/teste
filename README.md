# Pi
package com.mycompany.projectpi; // Nome do pacote corrigido

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.io.File;

public class ProjectPi extends JFrame {
    private JTextField nomeAdministradorField;
    private JPasswordField passwordField;
    private JButton entrarButton;
    private JButton sairButton;

    public ProjectPi() {
        initUI();
    }

    private void initUI() {
        setTitle("Memória Alegre - Login");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(800, 600);
        setLocationRelativeTo(null);
        setResizable(false);

        // Ajusta tamanho e moldura das caixas de diálogo
        UIManager.put("OptionPane.minimumSize", new Dimension(300, 100));
        UIManager.put("OptionPane.border", BorderFactory.createEmptyBorder(5, 5, 5, 5));
        UIManager.put("OptionPane.messageForeground", Color.WHITE);
        UIManager.put("Panel.background", Color.DARK_GRAY);

        // Carrega a imagem de fundo com verificação
        String imagePath = "c:/Users/25.00961-4/Downloads/image0.jpeg"; // Caminho absoluto
        File imageFile = new File(imagePath);
        ImageIcon backgroundIcon = imageFile.exists() ? new ImageIcon(imagePath) : null;

        Image backgroundImage = (backgroundIcon != null) ? backgroundIcon.getImage() : null;

        // Painel principal com imagem de fundo
        BackgroundPanel mainPanel = new BackgroundPanel(backgroundImage);
        mainPanel.setLayout(new GridBagLayout());
        mainPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));

        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.anchor = GridBagConstraints.CENTER;

        // Campo Nome Administrador
        JLabel nomeLabel = new JLabel("Nome Administrador:");
        nomeLabel.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        nomeLabel.setHorizontalAlignment(SwingConstants.CENTER);
        gbc.gridx = 0;
        gbc.gridy = 1;
        gbc.gridwidth = 2;
        mainPanel.add(nomeLabel, gbc);

        nomeAdministradorField = new JTextField(20);
        nomeAdministradorField.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridy = 2;
        gbc.gridwidth = 2;
        mainPanel.add(nomeAdministradorField, gbc);

        // Campo Senha
        JLabel senhaLabel = new JLabel("Senha:");
        senhaLabel.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        senhaLabel.setHorizontalAlignment(SwingConstants.CENTER);
        gbc.gridx = 0;
        gbc.gridy = 3;
        gbc.gridwidth = 2;
        mainPanel.add(senhaLabel, gbc);

        passwordField = new JPasswordField(20);
        passwordField.setFont(new Font("Trebuchet MS", Font.PLAIN, 20));
        gbc.gridy = 4;
        gbc.gridwidth = 2;
        mainPanel.add(passwordField, gbc);

        // Painel de botões
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 20, 10));
        buttonPanel.setOpaque(false);

        Dimension buttonSize = new Dimension(120, 40); 

        entrarButton = new JButton("Entrar");
        entrarButton.setFont(new Font("Trebuchet MS", Font.BOLD, 14));
        entrarButton.setPreferredSize(buttonSize);
        entrarButton.setBackground(Color.BLUE);
        entrarButton.setForeground(Color.WHITE);
        entrarButton.addActionListener(this::entrarAction);
        buttonPanel.add(entrarButton);

        sairButton = new JButton("Sair");
        sairButton.setFont(new Font("Trebuchet MS", Font.BOLD, 14));
        sairButton.setPreferredSize(buttonSize);
        sairButton.setBackground(Color.RED);
        sairButton.setForeground(Color.WHITE);
        sairButton.addActionListener(this::sairAction);
        buttonPanel.add(sairButton);

        gbc.gridx = 0;
        gbc.gridy = 5;
        gbc.gridwidth = 2;
        mainPanel.add(buttonPanel, gbc);

        add(mainPanel);
    }

    private void entrarAction(ActionEvent evt) {
        String nome = nomeAdministradorField.getText();
        String senha = new String(passwordField.getPassword());

        if ("admin@email.com".equals(nome) && "admin".equals(senha)) {
            JOptionPane.showMessageDialog(null, "Login bem-sucedido!", "Sucesso", JOptionPane.INFORMATION_MESSAGE);
            this.dispose();
        } else {
            JOptionPane.showMessageDialog(null, "Credenciais inválidas!", "Erro de Login", JOptionPane.ERROR_MESSAGE);
        }
    }

    private void sairAction(ActionEvent evt) {
        int confirm = JOptionPane.showConfirmDialog(null, "Deseja realmente sair?", "Sair", JOptionPane.YES_NO_OPTION);

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

            System.out.println("Tela inicial sendo carregada...");
            ProjectPi tela = new ProjectPi();
            tela.setVisible(true);
        });
    }

    class BackgroundPanel extends JPanel {
        private Image image0;

        public BackgroundPanel(Image backgroundImage) {
            this.image0 = backgroundImage;
        }

        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            if (image0 != null) {
                g.drawImage(image0, 0, 0, getWidth(), getHeight(), this);
            }
        }
    }
}
