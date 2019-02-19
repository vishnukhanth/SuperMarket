 import java.awt.EventQueue;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JLabel;
import javax.swing.JOptionPane;

import java.awt.Font;
import javax.swing.JTextField;
import javax.swing.JButton;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import javax.swing.JComboBox;
import javax.swing.GroupLayout;
import javax.swing.GroupLayout.Alignment;
import javax.swing.JPasswordField;
import java.sql.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.Color;

public class LoginPage {
	public DateFormat dateTime = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
	private JFrame frame;
	private JTextField txtusername;
	private JPasswordField txtpass;
    public static Connection conn1 = null;
    public static Connection conn2 = null;
    public static Connection conn3 = null;
    public static Connection conn4 = null;
	public static String selected_branch;
	public  static  String usrname;
	public static String dateandtime;

	private JTextField textdate;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					LoginPage window = new LoginPage();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
	/**
	 * Create the application.
	 */
	public LoginPage() {
			initialize();
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 551, 349);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
		
		JPanel panel = new JPanel();
		
		JLabel lblUsername = new JLabel("USERNAME");
		lblUsername.setBounds(27, 109, 86, 19);
		lblUsername.setFont(new Font("Tahoma", Font.BOLD, 15));
		
		JLabel lblPassword = new JLabel("PASSWORD");
		lblPassword.setBounds(27, 160, 102, 25);
		lblPassword.setFont(new Font("Tahoma", Font.BOLD, 15));
		
		txtusername = new JTextField();
		txtusername.setBounds(176, 105, 173, 31);
		txtusername.setColumns(10);
		
		JComboBox<String> comboBox = new JComboBox<>();
		comboBox.setBounds(176, 210, 173, 31);
		comboBox.setFont(new Font("Stencil", Font.ITALIC, 14));
		
		comboBox.addItem("Branch 1");
		comboBox.addItem("Branch 2");
		comboBox.addItem("Branch 3");
		comboBox.setSelectedItem(null);
		
		textdate = new JTextField();
		textdate.setFont(new Font("Tahoma", Font.BOLD, 13));
		textdate.setEditable(false);
		textdate.setBounds(176, 50, 173, 31);
		panel.add(textdate);
		textdate.setColumns(10);
		
		Calendar cal = Calendar.getInstance();
	    textdate.setText(dateTime.format(cal.getTime()));
	    
	    JLabel lblLoginPage = new JLabel("LOGIN  PAGE");
	    lblLoginPage.setFont(new Font("Supercell-Magic", Font.BOLD, 14));
	    lblLoginPage.setBounds(185, 11, 142, 25);
	    panel.add(lblLoginPage);   
		
		
		
		JButton btnSubmit = new JButton("LOGIN");
		btnSubmit.setForeground(Color.WHITE);
		btnSubmit.setBackground(Color.BLUE);
		btnSubmit.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				int count=0,flag=0,flag1=0;
				String value = (String)comboBox.getSelectedItem();
			 	String user_type=null;
				String uname = txtusername.getText();
				 usrname = txtusername.getText();
				 selected_branch = (String) comboBox.getSelectedItem();
				@SuppressWarnings("deprecation")
				String pass = txtpass.getText();
				String query = "SELECT * FROM shopkeeper WHERE username = '"+uname+"'";
				if( value==null || usrname.equals("") || pass.equals("") )
				{   
					JOptionPane.showMessageDialog(null,"Please fill the details");
					flag1=1;
				}
				if(flag1==0)
				{
				try 
				{
					Class.forName("com.mysql.jdbc.Driver");
				    conn1 = DriverManager.getConnection("jdbc:mysql://35.226.17.36:3306/branch1","root","mangojuice");
			        conn2= DriverManager.getConnection("jdbc:mysql://35.226.17.36:3306/branch2","root","mangojuice");
			        conn3= DriverManager.getConnection("jdbc:mysql://35.226.17.36:3306/branch3","root","mangojuice");
			        conn4= DriverManager.getConnection("jdbc:mysql://35.226.17.36:3306/admin","root","mangojuice");
			        if(value.equals("Branch 1"))
			        {
			        Statement st1 = conn1.createStatement();
			        ResultSet rs1 = st1.executeQuery(query);
			        while(rs1.next())
			        {
			        	count++;
			        	user_type= rs1.getString("user_type");
			        	String dbpass = rs1.getString("pass");
			        	if(dbpass.equals(pass))
			        	{
			        		flag=1;
			        	}
			        }
			       }
			        else if(value.equals("Branch 2"))
			        {
			        Statement st2 = conn2.createStatement();
			        ResultSet rs2 = st2.executeQuery(query);
			        while(rs2.next())
			        {
			        	count++;
			        	user_type= rs2.getString("user_type");
			        	 String dbpass = rs2.getString("pass");
				        	if(dbpass.equals(pass))
				        	{
				        		flag=1;
				        	}
			        }   
			        }
			        else
			        {
			        Statement st3 = conn3.createStatement();
			        ResultSet rs3 = st3.executeQuery(query);
			        while(rs3.next())
			        {
			        	count++;
			        	user_type= rs3.getString("user_type");
			        	 String dbpass = rs3.getString("pass");
				        	if(dbpass.equals(pass))
				        	{
				        		flag=1;
				        	}
			        }
			      } 
			       
				}catch(Exception e)
				{ 
					JOptionPane.showMessageDialog(null,e);
				}
				if(count ==1 && flag==1) {
				    JOptionPane.showMessageDialog(null,"Correct Username and password"); 
				    dateandtime = textdate.getText();
				    if(user_type.equals("shopkeeper"))
				    {
				    	frame.dispose();
				    	Billing.main(null);
				    }
				    else if(user_type.equals("admin"))
				    {
				    	frame.dispose();
				    	HeadAdmin.main(null);
				    }
				    else
				    {
				    	frame.dispose();
         		    	BranchAdmin.main(null);
				    }
				    
				}
				else if (count >1)
				{
					JOptionPane.showMessageDialog(null,"Duplicate username and Password");
				}
				else
				{
				    JOptionPane.showMessageDialog(null,"Wrong username or Password"); 
				}
				
			 }
			}
		});
		btnSubmit.setBounds(176, 262, 121, 37);
		btnSubmit.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseClicked(MouseEvent arg0) {
			}
		});
		btnSubmit.setFont(new Font("Tahoma", Font.BOLD, 14));
		GroupLayout groupLayout = new GroupLayout(frame.getContentPane());
		groupLayout.setHorizontalGroup(
			groupLayout.createParallelGroup(Alignment.LEADING)
				.addComponent(panel, GroupLayout.DEFAULT_SIZE, 434, Short.MAX_VALUE)
		);
		groupLayout.setVerticalGroup(
			groupLayout.createParallelGroup(Alignment.LEADING)
				.addComponent(panel, GroupLayout.DEFAULT_SIZE, 261, Short.MAX_VALUE)
		);
		panel.setLayout(null);
		panel.add(lblUsername);
		panel.add(lblPassword);
		panel.add(txtusername);
		panel.add(comboBox);
		panel.add(btnSubmit);
		
		txtpass = new JPasswordField();
		txtpass.setBounds(176, 159, 173, 31);
		panel.add(txtpass);
		frame.getContentPane().setLayout(groupLayout);
		
		JLabel lblDate = new JLabel("DATE");
		lblDate.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblDate.setBounds(27, 57, 86, 19);
		panel.add(lblDate);
		 
	    	  
	}
	
}
