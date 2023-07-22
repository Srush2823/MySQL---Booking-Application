package Cab_Booking_DBMS;


import javax.swing.*;
import javax.swing.border.EmptyBorder;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Cancel extends JFrame implements ActionListener{

    private JPanel contentPane;
    JButton btnYes;
    JButton btnNo;
    JLabel cnl;
    private JPanel pan1;

    /**
     * Launch the application.
     */
    public static void main(String[] args) {
        EventQueue.invokeLater(new Runnable() {
            public void run() {
                try {
                    Cancel frame = new Cancel();
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
    public Cancel() {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setBounds(100, 100, 450, 309);
        contentPane = new JPanel();
        contentPane.setBackground(new Color(169, 169, 169));
        contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
        setResizable(false);

        setContentPane(contentPane);
        contentPane.setLayout(null);

        JLabel lblNewLabel = new JLabel("Are you sure? Do you want to cancel cab?");
        lblNewLabel.setFont(new Font("Verdana", Font.PLAIN, 15));
        lblNewLabel.setForeground(new Color(0, 0, 0));
        lblNewLabel.setBounds(53, 34, 336, 41);
        contentPane.add(lblNewLabel);

        btnYes = new JButton("No");
        btnYes.setBackground(new Color(105, 105, 105));
        btnYes.setForeground(new Color(0, 0, 0));
        btnYes.setFont(new Font("Verdana", Font.BOLD, 14));
        btnYes.setBounds(53, 108, 117, 41);
        btnYes.addActionListener(this);
        contentPane.add(btnYes);

        btnNo = new JButton("Yes");
        btnNo.setBackground(new Color(105, 105, 105));
        btnNo.setForeground(new Color(0, 0, 0));
        btnNo.setFont(new Font("Verdana", Font.BOLD, 14));
        btnNo.setBounds(244, 108, 117, 41);
        btnNo.addActionListener(this);
        contentPane.add(btnNo);

        pan1 = new JPanel();
        pan1.setBackground(new Color(169, 169, 169));
        pan1.setBounds(53, 174, 320, 64);
        contentPane.add(pan1);
        pan1.setLayout(null);

        cnl = new JLabel("Cancelled Successfully!");
        cnl.setBackground(new Color(169, 169, 169));
        cnl.setBounds(10, 10, 289, 35);
        pan1.add(cnl);
        cnl.setHorizontalAlignment(SwingConstants.CENTER);
        cnl.setFont(new Font("Verdana", Font.PLAIN, 15));
        cnl.setForeground(new Color(0, 0, 0));
        pan1.setVisible(false);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        // TODO Auto-generated method stub
        if(e.getSource()==btnNo) {


            pan1.setVisible(true);
        }
        else if(e.getSource()==btnYes){


            this.dispose();
        }

    }
}
