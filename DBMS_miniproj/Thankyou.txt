package Cab_Booking_DBMS;

import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import java.awt.Color;
import javax.swing.JLabel;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.SwingConstants;
import javax.swing.JButton;

public class ThankYou extends JFrame implements ActionListener{

    private JPanel contentPane;
    JButton cnbtn;
    JButton btnClose;

    /**
     * Launch the application.
     */
    public static void main(String[] args) {
        EventQueue.invokeLater(new Runnable() {
            public void run() {
                try {
                    ThankYou frame = new ThankYou();
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
    public ThankYou() {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setBounds(100, 100, 450, 300);
        contentPane = new JPanel();
        contentPane.setBackground(new Color(192, 192, 192));
        contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
        setResizable(false);

        setContentPane(contentPane);
        contentPane.setLayout(null);

        JLabel lblNewLabel = new JLabel("Your cab is arriving shortly...");
        lblNewLabel.setForeground(new Color(0, 0, 0));
        lblNewLabel.setFont(new Font("Yu Gothic", Font.BOLD, 17));
        lblNewLabel.setHorizontalAlignment(SwingConstants.CENTER);
        lblNewLabel.setBounds(65, 76, 301, 29);
        contentPane.add(lblNewLabel);

        JLabel lblNewLabel_1 = new JLabel("Booking Confirmed!");
        lblNewLabel_1.setForeground(new Color(0, 0, 0));
        lblNewLabel_1.setFont(new Font("Yu Gothic", Font.BOLD, 20));
        lblNewLabel_1.setHorizontalAlignment(SwingConstants.CENTER);
        lblNewLabel_1.setBounds(108, 43, 221, 29);
        contentPane.add(lblNewLabel_1);

        cnbtn = new JButton("Cancel");
        cnbtn.setBackground(new Color(105, 105, 105));
        cnbtn.setForeground(new Color(0, 0, 0));
        cnbtn.setFont(new Font("Verdana", Font.BOLD, 14));
        cnbtn.setBounds(31, 158, 154, 37);
        cnbtn.addActionListener(this);
        contentPane.add(cnbtn);

        btnClose = new JButton("Close");
        btnClose.setBackground(new Color(105, 105, 105));
        btnClose.setForeground(new Color(0, 0, 0));
        btnClose.setFont(new Font("Verdana", Font.BOLD, 14));
        btnClose.setBounds(228, 158, 154, 37);
        btnClose.addActionListener(this);
        contentPane.add(btnClose);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        // TODO Auto-generated method stub
        if(e.getSource()==btnClose) {
            this.dispose();
        }
        else if(e.getSource()==cnbtn) {
            this.dispose();
            new Cancel().setVisible(true);
        }
    }
}

