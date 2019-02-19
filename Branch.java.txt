import java.awt.EventQueue;
import java.sql.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;

import javax.swing.JFrame;
import java.awt.CardLayout;
import javax.swing.JPanel;
import javax.swing.table.DefaultTableModel;

import net.proteanit.sql.DbUtils;

import javax.swing.JLabel;
import javax.swing.JOptionPane;

import java.awt.Font;
import javax.swing.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.Color;

public class BranchAdmin extends LoginPage{

	public DateFormat dateTime = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
	private JFrame frame;
	private JTextField textdate;
	private JTextField textusername;
	private JTextField name;
	private JTextField mobileno;
	private JTextField address;
	private JTextField textusrname;
	private JTextField textField_6;
	private JTable table;
	private JTable stocktable;
	private JPasswordField txtpass;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					BranchAdmin window = new BranchAdmin();
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
	public BranchAdmin() {
		initialize();
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 650, 435);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(new CardLayout(0, 0));
		
		JPanel branchadminpage = new JPanel();
		frame.getContentPane().add(branchadminpage, "name_951703999207457");
		branchadminpage.setLayout(null);
		
		JLabel lblBranchAdmin = new JLabel("BRANCH  ADMIN ");
		lblBranchAdmin.setFont(new Font("Supercell-Magic", Font.BOLD, 17));
		lblBranchAdmin.setBounds(209, 23, 226, 34);
		branchadminpage.add(lblBranchAdmin);
		
		JLabel lblDate = new JLabel("DATE  :");
		lblDate.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblDate.setBounds(40, 70, 113, 26);
		branchadminpage.add(lblDate);
		
		JLabel lblUsername = new JLabel("USERNAME :");
		lblUsername.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblUsername.setBounds(40, 125, 113, 26);
		branchadminpage.add(lblUsername);
		
		textdate = new JTextField();
		textdate.setFont(new Font("Tahoma", Font.BOLD, 14));
		textdate.setEditable(false);
		textdate.setBounds(151, 72, 189, 26);
		branchadminpage.add(textdate);
		textdate.setColumns(10);
		Calendar cal = Calendar.getInstance();
	    textdate.setText(dateTime.format(cal.getTime()));
		
		textusername = new JTextField();
		textusername.setFont(new Font("Tahoma", Font.BOLD, 14));
		textusername.setEditable(false);
		textusername.setBounds(151, 127, 189, 26);
		branchadminpage.add(textusername);
		textusername.setColumns(10);
		textusername.setText(usrname);
		
		JButton btnLogOut = new JButton("LOG OUT");
		btnLogOut.setBackground(Color.DARK_GRAY);
		btnLogOut.setForeground(Color.WHITE);
		btnLogOut.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				try {
					String queryy = "INSERT INTO loginDetails(username,logintime,logout_time)VALUES(?,?,?)";
					PreparedStatement ps4 = conn4.prepareStatement(queryy);
					ps4.setString(1,usrname);
					ps4.setString(2,dateandtime);
					ps4.setString(3,dateTime.format(cal.getTime()));
					ps4.executeUpdate();
				}
				catch(Exception e6)
				{
					JOptionPane.showMessageDialog(null,e6);
				}
				frame.dispose();
				LoginPage.main(null);
			}
		});
		btnLogOut.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnLogOut.setBounds(259, 347, 113, 35);
		branchadminpage.add(btnLogOut);
		
		JPanel addshopkeeper = new JPanel();
		frame.getContentPane().add(addshopkeeper, "name_951708925020682");
		addshopkeeper.setLayout(null);
		
		JLabel lblAddShopkeeper = new JLabel("ADD SHOPKEEPER");
		lblAddShopkeeper.setFont(new Font("Supercell-Magic", Font.BOLD, 17));
		lblAddShopkeeper.setBounds(185, 11, 247, 41);
		addshopkeeper.add(lblAddShopkeeper);
		
		JLabel lblName = new JLabel("Name");
		lblName.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblName.setBounds(47, 85, 99, 25);
		addshopkeeper.add(lblName);
		
		JLabel lblMobileNo = new JLabel("Mobile no");
		lblMobileNo.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblMobileNo.setBounds(47, 139, 99, 25);
		addshopkeeper.add(lblMobileNo);
		
		JLabel lblNewLabel = new JLabel("Address");
		lblNewLabel.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblNewLabel.setBounds(47, 192, 99, 25);
		addshopkeeper.add(lblNewLabel);
		
		JLabel lblUsername_1 = new JLabel("Username");
		lblUsername_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblUsername_1.setBounds(47, 243, 99, 25);
		addshopkeeper.add(lblUsername_1);
		
		JLabel lblPassword = new JLabel("Password");
		lblPassword.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblPassword.setBounds(47, 292, 99, 25);
		addshopkeeper.add(lblPassword);
		
		name = new JTextField();
		name.setBounds(180, 83, 160, 29);
		addshopkeeper.add(name);
		name.setColumns(10);
		
		mobileno = new JTextField();
		mobileno.setBounds(180, 139, 160, 29);
		addshopkeeper.add(mobileno);
		mobileno.setColumns(10);
		
		address = new JTextField();
		address.setBounds(181, 192, 159, 29);
		addshopkeeper.add(address);
		address.setColumns(10);
		
		textusrname = new JTextField();
		textusrname.setBounds(180, 243, 160, 29);
		addshopkeeper.add(textusrname);
		textusrname.setColumns(10);
		
		JButton btnAddShopkeeper_1 = new JButton("ADD SHOPKEEPER");
		btnAddShopkeeper_1.addActionListener(new ActionListener() {
			@SuppressWarnings({ "deprecation", "unlikely-arg-type" })
			public void actionPerformed(ActionEvent e) {
				int flag=0;
				if(name.getText().equals("") || mobileno.getText().equals("")|| address.equals("") || textusrname.getText().equals("") || txtpass.getText().equals("") )
				{
					JOptionPane.showMessageDialog(null,"Please fill all the fields");
					flag=1;
				}
				if(flag==0)
			{
					try {
					String query = "INSERT INTO shopkeeper(name,phone_no,username,pass,address,user_type)VALUES(?,?,?,?,?,?)";
					PreparedStatement ps3 = null;
					if(selected_branch == "Branch 1")
					{
						ps3 = conn1.prepareStatement(query);
					}
					else if(selected_branch == "Branch 2")
					{
						ps3 = conn2.prepareStatement(query);
					}
					else
					{
						ps3 = conn3.prepareStatement(query);
					}
					ps3.setString(1,name.getText());
					ps3.setString(2,mobileno.getText());
					ps3.setString(3,textusrname.getText());
					ps3.setString(4,txtpass.getText());
					ps3.setString(5,address.getText());
					ps3.setString(6,"shopkeeper");
					ps3.executeUpdate();
					JOptionPane.showMessageDialog(null,"shopkeeper added successfully !!");					
					name.setText("");
					mobileno.setText("");
					textusrname.setText("");
					txtpass.setText("");
					address.setText("");
			}
					catch(Exception e4)
					{
						JOptionPane.showMessageDialog(null,e4);
					}
			}
					
			}
		});
		btnAddShopkeeper_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnAddShopkeeper_1.setBounds(180, 343, 199, 42);
		addshopkeeper.add(btnAddShopkeeper_1);
		
		JButton btnGoBack = new JButton("GO BACK");
		btnGoBack.setForeground(Color.WHITE);
		btnGoBack.setBackground(Color.BLUE);
		btnGoBack.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				addshopkeeper.setVisible(false);
				branchadminpage.setVisible(true);
				name.setText("");
				mobileno.setText("");
				textusrname.setText("");
				txtpass.setText("");
				address.setText("");
			}
		});
		btnGoBack.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack.setBounds(421, 343, 106, 38);
		addshopkeeper.add(btnGoBack);
		
		txtpass = new JPasswordField();
		txtpass.setBounds(180, 292, 160, 29);
		addshopkeeper.add(txtpass);
		
		JPanel removeshopkeeper = new JPanel();
		frame.getContentPane().add(removeshopkeeper, "name_951714370717521");
		removeshopkeeper.setLayout(null);
		
		JLabel lblRemoveShopkeeper = new JLabel("REMOVE  SHOPKEEPER");
		lblRemoveShopkeeper.setFont(new Font("Supercell-Magic", Font.BOLD, 17));
		lblRemoveShopkeeper.setBounds(176, 11, 301, 33);
		removeshopkeeper.add(lblRemoveShopkeeper);
		
		JLabel lblName_1 = new JLabel("Name       :");
		lblName_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblName_1.setBounds(124, 99, 115, 33);
		removeshopkeeper.add(lblName_1);
		
		textField_6 = new JTextField();
		textField_6.setBounds(265, 99, 173, 33);
		removeshopkeeper.add(textField_6);
		textField_6.setColumns(10);
		
		JButton btnDeleteShopkeeper = new JButton("DELETE SHOPKEEPER");
		btnDeleteShopkeeper.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				int flag=0;
				if(textField_6.getText().equals(""))
				{
					JOptionPane.showMessageDialog(null,"Please fill all fields");
					flag = 1;
				}
				if(flag==0)
				{
					String uname = textField_6.getText();
				try { 
				String qry = "DELETE FROM shopkeeper WHERE name =?";
				PreparedStatement ps1 = null;
				if(selected_branch=="Branch 1")
				{
				  ps1 = conn1.prepareStatement(qry);
				}
				else if(selected_branch=="Branch 2")
				{
					ps1 = conn2.prepareStatement(qry);
				}
				else
				{
				   ps1 = conn3.prepareStatement(qry);
				}
				   ps1.setString(1,uname);
		           int check = ps1.executeUpdate();
		           //check has the no of affected or delted rows..
		           if(check == 0)
		           {
		        	   JOptionPane.showMessageDialog(null,"Enter correct shopkeeper name"); 
		           }
		           else
		           {
		           JOptionPane.showMessageDialog(null,"Shopkeeper removed successfully !!");
		           }
		           textField_6.setText("");
				}
				catch(Exception e0)
				{
					JOptionPane.showMessageDialog(null,e0);
				}
			}
		}
		});
		btnDeleteShopkeeper.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnDeleteShopkeeper.setBounds(265, 189, 209, 38);
		removeshopkeeper.add(btnDeleteShopkeeper);
		
		JButton btnGoBack_1 = new JButton("GO BACK");
		btnGoBack_1.setBackground(Color.BLUE);
		btnGoBack_1.setForeground(Color.WHITE);
		btnGoBack_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				removeshopkeeper.setVisible(false);
				branchadminpage.setVisible(true);
				textField_6.setText("");
			}
		});
		btnGoBack_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_1.setBounds(265, 280, 104, 33);
		removeshopkeeper.add(btnGoBack_1);
		
		JPanel stockdetails = new JPanel();
		frame.getContentPane().add(stockdetails, "name_953702023938647");
		stockdetails.setLayout(null);
		
		JScrollPane scrollPane_1 = new JScrollPane();
		scrollPane_1.setBounds(36, 60, 524, 270);
		stockdetails.add(scrollPane_1);
		
		stocktable = new JTable();
		stocktable.setFont(new Font("Tahoma", Font.BOLD, 15));
		stocktable.setRowSelectionAllowed(false);
		stocktable.setEnabled(false);
		scrollPane_1.setViewportView(stocktable);
		
		JPanel logindetails = new JPanel();
		frame.getContentPane().add(logindetails, "name_953723007478750");
		logindetails.setLayout(null);
		
		JScrollPane scrollPane = new JScrollPane();
		scrollPane.setBounds(31, 47, 548, 263);
		logindetails.add(scrollPane);
		
		table = new JTable();
		table.setFont(new Font("Tahoma", Font.BOLD, 15));
		table.setRowSelectionAllowed(false);
		table.setEnabled(false);
		scrollPane.setViewportView(table);
		
		JButton btnGoBack_3 = new JButton("GO BACK");
		btnGoBack_3.setForeground(Color.WHITE);
		btnGoBack_3.setBackground(Color.BLUE);
		btnGoBack_3.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockdetails.setVisible(false);
				branchadminpage.setVisible(true);
			}
		});
		btnGoBack_3.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_3.setBounds(267, 350, 106, 35);
		stockdetails.add(btnGoBack_3);
		
		JButton btnViewStockDetails = new JButton("VIEW STOCK DETAILS");
		btnViewStockDetails.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				branchadminpage.setVisible(false);
				stockdetails.setVisible(true);
				try {
					String query = "SELECT * FROM items";
					Statement s1 = null;
					if(selected_branch=="Branch 1")
					{
						s1 = conn1.createStatement();
					}
					else if(selected_branch=="Branch 2")
					{
						s1 = conn2.createStatement();
					}
					else
					{
						s1 = conn3.createStatement();
					}
					ResultSet rs1 = s1.executeQuery(query);
					stocktable.setModel(DbUtils.resultSetToTableModel(rs1));		
				}
				catch(Exception s)
				{
					JOptionPane.showMessageDialog(null,s);
				}
				
			}
		});
		btnViewStockDetails.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnViewStockDetails.setBounds(209, 302, 211, 34);
		branchadminpage.add(btnViewStockDetails);
		
		JButton btnGoBack_2 = new JButton("GO BACK");
		btnGoBack_2.setForeground(Color.WHITE);
		btnGoBack_2.setBackground(Color.BLUE);
		btnGoBack_2.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				branchadminpage.setVisible(true);
				logindetails.setVisible(false);
			}
		});
		btnGoBack_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_2.setBounds(265, 329, 112, 34);
		logindetails.add(btnGoBack_2);
		
		JButton btnViewLoginDetails = new JButton("VIEW LOGIN DETAILS");
		btnViewLoginDetails.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				DefaultTableModel model = new DefaultTableModel();
				Object[] columns = {"Username","Login_time","Logout_time"};
				model.setColumnIdentifiers(columns);
				table.setModel(model);
			    Object[]  row = new Object[3];
			    try
			  {
			    String usrtype,username;
			    String query1 = "SELECT * FROM shopkeeper";
			    String query2 = "SELECT * FROM loginDetails WHERE username=?";
			    PreparedStatement ps2 = null;
				PreparedStatement ps1 = null;
				ResultSet rs2 = null;
				ResultSet rs1 = null;
				ps2= conn4.prepareStatement(query2);
				if(selected_branch=="Branch 1")
				{
					ps1 = conn1.prepareStatement(query1);
				}
				else if(selected_branch=="Branch 2")
				{
					ps1 = conn2.prepareStatement(query1);
				}
				else
				{
					ps1 = conn3.prepareStatement(query1);
				}
				rs1 = ps1.executeQuery();
				while(rs1.next())
				{
					usrtype = rs1.getString("user_type");
					username = rs1.getString("username");
					if(usrtype.equals("admin"))
					{
						continue;
					}
					else
					{
						ps2.setString(1,username);
						rs2 = ps2.executeQuery();
						String username1,login,logout;
						while(rs2.next())
						{
						username1 = rs2.getString("username");
						login =rs2.getString("logintime");
						logout = rs2.getString("logout_time");
						row[0] = username1;
						row[1] = login;
						row[2] = logout;
						model.addRow(row);
						}	
						
					}
				}
		    }
			    catch(Exception e2)
			    {
			    	JOptionPane.showMessageDialog(null,e2);
			    }
			    logindetails.setVisible(true);
			    branchadminpage.setVisible(false);
			}
		});
		btnViewLoginDetails.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnViewLoginDetails.setBounds(209, 256, 211, 35);
		branchadminpage.add(btnViewLoginDetails);
		
		JButton btnAddShopkeeper = new JButton("ADD SHOPKEEPER");
		btnAddShopkeeper.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				branchadminpage.setVisible(false);
				addshopkeeper.setVisible(true);
			}
		});
		btnAddShopkeeper.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnAddShopkeeper.setBounds(209, 164, 211, 34);
		branchadminpage.add(btnAddShopkeeper);
		
		JButton btnRemoveShopkeeper = new JButton("REMOVE SHOPKEEPER");
		btnRemoveShopkeeper.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				branchadminpage.setVisible(false);
				removeshopkeeper.setVisible(true);
			}
		});
		btnRemoveShopkeeper.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnRemoveShopkeeper.setBounds(209, 209, 211, 36);
		branchadminpage.add(btnRemoveShopkeeper);
	}
}
