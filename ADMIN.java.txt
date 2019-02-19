import java.awt.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.awt.Font;

import net.proteanit.sql.DbUtils;

import java.awt.event.ActionListener;
import java.sql.*;
import java.awt.event.ActionEvent;
import java.awt.CardLayout;
import javax.swing.*;


public class HeadAdmin extends LoginPage
{

	private JFrame frame;
	
	private static final DateFormat dateTime = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
	private JTable table;
	private JTable table_1;
	private JTextField textField;
	private JTextField textField_1;
	private JTextField textField_2;
	private JTextField textField_3;
	private JTextField text_id;
	private JTextField text_quantity;
	private JTextField text_price;
	public static int databaseqty;
	private JTextField textField_4;
	private JTextField textField_5;
	private JTextField textField_6;
	private JTable table_2;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					HeadAdmin window = new HeadAdmin();
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
	public HeadAdmin() {
		initialize();
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 647, 443);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(new CardLayout(0, 0));
		
		JPanel adminpage = new JPanel();
		frame.getContentPane().add(adminpage, "name_421050764026480");
		adminpage.setLayout(null);
		
		JPanel stockpage;
		stockpage = new JPanel();
		
		JLabel lblHeadAdmin = new JLabel("HEAD ADMIN");
		lblHeadAdmin.setFont(new Font("Supercell-Magic", Font.BOLD, 18));
		lblHeadAdmin.setBounds(229, 11, 216, 42);
		adminpage.add(lblHeadAdmin);
		
		JLabel lblDate = new JLabel("Date");
		lblDate.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblDate.setBounds(35, 63, 89, 27);
		adminpage.add(lblDate);
		
		JLabel lblUsername = new JLabel("Username");
		lblUsername.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblUsername.setBounds(35, 108, 105, 33);
		adminpage.add(lblUsername);
		
		JTextArea Dateandtime = new JTextArea();
		Dateandtime.setEditable(false);
		Dateandtime.setFont(new Font("Tahoma", Font.BOLD, 15));
		Dateandtime.setBounds(147, 64, 183, 33);
		adminpage.add(Dateandtime);
		
		JTextArea Username = new JTextArea();
		Username.setFont(new Font("Tahoma", Font.BOLD, 16));
		Username.setEditable(false);
		Username.setBounds(147, 110, 183, 27);
		adminpage.add(Username);
		Username.setText(usrname);
		

		frame.getContentPane().add(stockpage, "name_421055254182372");
		stockpage.setLayout(null);
		
		JLabel lblStockControl = new JLabel("STOCK CONTROL");
		lblStockControl.setFont(new Font("Supercell-Magic", Font.BOLD, 17));
		lblStockControl.setBounds(220, 11, 231, 34);
		stockpage.add(lblStockControl);
		
		JLabel lblBranch = new JLabel("Branch 1 :");
		lblBranch.setFont(new Font("Tahoma", Font.BOLD, 14));
		lblBranch.setBounds(60, 286, 84, 25);
		stockpage.add(lblBranch);
		
		JLabel lblBranch_1 = new JLabel("Branch 2 :");
		lblBranch_1.setFont(new Font("Tahoma", Font.BOLD, 14));
		lblBranch_1.setBounds(60, 319, 84, 27);
		stockpage.add(lblBranch_1);
		
		JLabel lblBranch_2 = new JLabel("Branch 3 :");
		lblBranch_2.setFont(new Font("Tahoma", Font.BOLD, 14));
		lblBranch_2.setBounds(60, 357, 84, 22);
		stockpage.add(lblBranch_2);
		
		JLabel lblStockAvailability = new JLabel("STOCK AVAILABILITY");
		lblStockAvailability.setFont(new Font("Supercell-Magic", Font.BOLD, 14));
		lblStockAvailability.setBounds(53, 250, 231, 22);
		stockpage.add(lblStockAvailability);
		
		JLabel label = new JLabel("");
		label.setFont(new Font("Tahoma", Font.BOLD, 15));
		label.setBounds(144, 290, 107, 21);
		stockpage.add(label);
		
		JLabel label_1 = new JLabel("");
		label_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		label_1.setBounds(144, 323, 107, 23);
		stockpage.add(label_1);
		
		JLabel label_2 = new JLabel("");
		label_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		label_2.setBounds(144, 357, 107, 24);
		stockpage.add(label_2);
		
		JButton btnBack = new JButton("GO BACK\r\n");
		btnBack.setForeground(Color.WHITE);
		btnBack.setBackground(Color.BLUE);
		btnBack.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				adminpage.setVisible(true);
				stockpage.setVisible(false);
			}
		});
		btnBack.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnBack.setBounds(411, 353, 112, 34);
		stockpage.add(btnBack);

		Calendar cal = Calendar.getInstance();
		Dateandtime.setText(dateTime.format(cal.getTime()));
		
		JPanel viewdetails = new JPanel();
		frame.getContentPane().add(viewdetails, "name_861083623465840");
		viewdetails.setLayout(null);
		
		JScrollPane scrollPane = new JScrollPane();
		scrollPane.setEnabled(false);
		scrollPane.setBounds(22, 21, 547, 329);
		viewdetails.add(scrollPane);
		
		table = new JTable();
		table.setRowSelectionAllowed(false);
		table.setFont(new Font("Tahoma", Font.BOLD, 14));
		table.setEnabled(false);
		scrollPane.setViewportView(table);
		
		JButton btnGoBack = new JButton("GO BACK");
		btnGoBack.setForeground(Color.WHITE);
		btnGoBack.setBackground(Color.BLUE);
		btnGoBack.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				viewdetails.setVisible(false);
				adminpage.setVisible(true);
			}
		});
		btnGoBack.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack.setBounds(262, 361, 124, 32);
		viewdetails.add(btnGoBack);
		
		JPanel viewdetailsstock = new JPanel();
		frame.getContentPane().add(viewdetailsstock, "name_752269781179238");
		viewdetailsstock.setLayout(null);
		
		JScrollPane scrollPane_1 = new JScrollPane();
		scrollPane_1.setBounds(10, 11, 568, 328);
		viewdetailsstock.add(scrollPane_1);
		
		table_1 = new JTable();
		table_1.setFont(new Font("Tahoma", Font.BOLD, 14));
		table_1.setRowSelectionAllowed(false);
		table_1.setEnabled(false);
		scrollPane_1.setViewportView(table_1);
		
		JButton btnGoBack_1 = new JButton("GO BACK");
		btnGoBack_1.setForeground(Color.WHITE);
		btnGoBack_1.setBackground(Color.BLUE);
		btnGoBack_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(true);
				viewdetailsstock.setVisible(false);	
			}
		});
		btnGoBack_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_1.setBounds(277, 359, 110, 34);
		viewdetailsstock.add(btnGoBack_1);
		
		JButton btnNewButton_1 = new JButton("VIEW LOGIN DETAILS");
		btnNewButton_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
	            try {
	            	String loginquery = "SELECT * FROM loginDetails";
					PreparedStatement  ps1 = conn4.prepareStatement(loginquery);
					ResultSet rs1 = ps1.executeQuery();
					table.setModel(DbUtils.resultSetToTableModel(rs1));	
					viewdetails.setVisible(true);
					adminpage.setVisible(false);
					viewdetailsstock.setVisible(false);
					stockpage.setVisible(false);
				} catch (SQLException e1) {
					JOptionPane.showMessageDialog(null,e1);
				}

			}
		});
		btnNewButton_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_1.setBounds(180, 214, 244, 42);
		adminpage.add(btnNewButton_1);
		
		JButton btnNewButton_2 = new JButton("STOCK MANAGEMENT\r\n");
		btnNewButton_2.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				adminpage.setVisible(false);
				stockpage.setVisible(true);
			}
			
		});
		btnNewButton_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_2.setBounds(180, 275, 244, 42);
		adminpage.add(btnNewButton_2);
		
		JButton btnLogOut = new JButton("LOG OUT");
		btnLogOut.setForeground(Color.WHITE);
		btnLogOut.setBackground(Color.RED);
		btnLogOut.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				try {
					String query ="INSERT INTO loginDetails(username,logintime,logout_time)VALUES(?,?,?)";
					PreparedStatement ps1 = conn4.prepareStatement(query);
					ps1.setString(1,usrname);
					ps1.setString(2,dateandtime);
					ps1.setString(3,Dateandtime.getText());
					ps1.executeUpdate();	
				} catch (SQLException e) {
					JOptionPane.showMessageDialog(null,e);
				}
				frame.dispose();
				LoginPage.main(null);
			}
		});
		btnLogOut.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnLogOut.setBounds(243, 344, 105, 33);
		adminpage.add(btnLogOut);
		
		JButton btnNewButton = new JButton("VIEW CUSTOMER DETAILS\r\n");
		btnNewButton.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton.setBounds(180, 155, 244, 42);
		adminpage.add(btnNewButton);
		btnNewButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					String query1 = "SELECT * FROM customer_details";
					PreparedStatement st1 = null;
					if(selected_branch=="Branch 1")
					{
					  st1 = conn1.prepareStatement(query1);
					}
					else if(selected_branch=="Branch 2")
					{
					  st1 = conn2.prepareStatement(query1);
					}
					else 
					{
					  st1 = conn3.prepareStatement(query1);
					}	
					ResultSet rst1 = st1.executeQuery();
					table.setModel(DbUtils.resultSetToTableModel(rst1));	
					viewdetails.setVisible(true);
					adminpage.setVisible(false);
					viewdetailsstock.setVisible(false);
					stockpage.setVisible(false);
				} catch (SQLException e1)
				{
					JOptionPane.showMessageDialog(null,e1);
				}
			}
		});	
		
		JButton btnNewButton_3 = new JButton("VIEW STOCK\r\n");
		btnNewButton_3.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_3.setBounds(220, 44, 231, 39);
		stockpage.add(btnNewButton_3);
		btnNewButton_3.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
			try
			{
				String query2 = "SELECT * FROM items";
				PreparedStatement ps1 = null;
				if(selected_branch=="Branch 1")
				{
				  ps1 = conn1.prepareStatement(query2);
				}
				else if(selected_branch=="Branch 2")
				{
				  ps1 = conn2.prepareStatement(query2);
				}
				else 
				{
				  ps1 = conn3.prepareStatement(query2);
				}	
				ResultSet rs2 = ps1.executeQuery();
				table_1.setModel(DbUtils.resultSetToTableModel(rs2));
				viewdetailsstock.setVisible(true);
				stockpage.setVisible(false);
			}
				catch (Exception e3)
				{
					JOptionPane.showMessageDialog(null,e3);
				}
			}
		});
		
		JButton btnCheck = new JButton("CHECK");
		btnCheck.setFont(new Font("Tahoma", Font.BOLD, 13));
		btnCheck.setBounds(261, 286, 89, 26);
		stockpage.add(btnCheck);
		btnCheck.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					int flag = 0;
					String qry = "SELECT * FROM items";
					Statement s1 = null;
					s1 = conn1.createStatement();
					ResultSet rs1 = s1.executeQuery(qry);
					while(rs1.next())
					{
						int Quantity = rs1.getInt("quantity");
						if(Quantity <= 5)
						{
							flag = 1;
						}
					}
					if(flag == 1)
					{
						label.setText("Low Stock");
					}
					else
					{
						label.setText("Available");
					}
				}
				catch(Exception e4)
				{
					JOptionPane.showMessageDialog(null,e4);
				}
			}
		});
		
		JButton btnCheck_1 = new JButton("CHECK");
		btnCheck_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					int flag = 0;
					String qry = "SELECT * FROM items";
					Statement s1 = null;
					s1 = conn2.createStatement();
					ResultSet rs1 = s1.executeQuery(qry);
					while(rs1.next())
					{
						int Quantity = rs1.getInt("quantity");
						if(Quantity <= 5)
						{
							flag = 1;
						}
					}
					if(flag == 1)
					{
						label_1.setText("Low Stock");
					}
					else
					{
						label_1.setText("Available");
					}
				}
				catch(Exception e4)
				{
					JOptionPane.showMessageDialog(null,e4);
				}
			}
		});
		btnCheck_1.setFont(new Font("Tahoma", Font.BOLD, 13));
		btnCheck_1.setBounds(261, 323, 89, 25);
		stockpage.add(btnCheck_1);
		
		JButton btnCheck_2 = new JButton("CHECK");
		btnCheck_2.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					int flag = 0;
					String qry = "SELECT * FROM items";
					Statement s1 = null;
					s1 = conn3.createStatement();
					ResultSet rs1 = s1.executeQuery(qry);
					while(rs1.next())
					{
						int Quantity = rs1.getInt("quantity");
						if(Quantity <= 5)
						{
							flag = 1;
						}
					}
					if(flag == 1)
					{
						label_2.setText("Low Stock");
					}
					else
					{
						label_2.setText("Available");
					}
				}
				catch(Exception e4)
				{
					JOptionPane.showMessageDialog(null,e4);
				}
			}
		});
		btnCheck_2.setFont(new Font("Tahoma", Font.BOLD, 13));
		btnCheck_2.setBounds(261, 359, 89, 25);
		stockpage.add(btnCheck_2);
		
		JPanel newproduct = new JPanel();
		frame.getContentPane().add(newproduct, "name_879079065045911");
		newproduct.setLayout(null);
		
		JLabel lblProductId = new JLabel("Product ID");
		lblProductId.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblProductId.setBounds(39, 52, 121, 28);
		newproduct.add(lblProductId);
		
		JLabel lblProductName = new JLabel("Product name");
		lblProductName.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblProductName.setBounds(39, 108, 127, 28);
		newproduct.add(lblProductName);
		
		JLabel lblQuantity = new JLabel("Quantity");
		lblQuantity.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblQuantity.setBounds(39, 164, 121, 28);
		newproduct.add(lblQuantity);
		
		JLabel lblPrice = new JLabel("Price");
		lblPrice.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblPrice.setBounds(39, 224, 121, 28);
		newproduct.add(lblPrice);
		
		textField = new JTextField();
		textField.setFont(new Font("Tahoma", Font.BOLD, 13));
		textField.setBounds(188, 58, 155, 28);
		newproduct.add(textField);
		textField.setColumns(10);
		
		textField_1 = new JTextField();
		textField_1.setFont(new Font("Tahoma", Font.BOLD, 13));
		textField_1.setBounds(188, 114, 155, 28);
		newproduct.add(textField_1);
		textField_1.setColumns(10);
		
		textField_2 = new JTextField();
		textField_2.setFont(new Font("Tahoma", Font.BOLD, 13));
		textField_2.setBounds(188, 170, 155, 28);
		newproduct.add(textField_2);
		textField_2.setColumns(10);
		
		textField_3 = new JTextField();
		textField_3.setFont(new Font("Tahoma", Font.BOLD, 13));
		textField_3.setBounds(188, 224, 155, 28);
		newproduct.add(textField_3);
		textField_3.setColumns(10);
		
		JButton btnAddNewProduct = new JButton("ADD NEW PRODUCT");
		btnAddNewProduct.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				if(textField.getText().equals("")||  textField_1.getText().equals("") ||  textField_2.getText().equals("") ||  textField_3.getText().equals(""))
				{
					JOptionPane.showMessageDialog(null,"Please fill all fields");
				}
				else {
				try {
					String query = "INSERT INTO stock(item_id,item_name,master_stock,master_price)VALUES(?,?,?,?)";
					String query1 = "INSERT INTO items(item_id,item_name,quantity,discount,price)VALUES(?,?,?,?,?)";
					PreparedStatement ps1 = conn4.prepareStatement(query);
					PreparedStatement ps2 = conn1.prepareStatement(query1);
					PreparedStatement ps3 = conn2.prepareStatement(query1);
					PreparedStatement ps4 = conn3.prepareStatement(query1);
					ps1.setInt(1,Integer.parseInt(textField.getText()));
					ps1.setString(2,textField_1.getText());
					ps1.setInt(3,Integer.parseInt(textField_2.getText()));
					ps1.setDouble(4,Double.parseDouble(textField_3.getText()));		
					ps1.executeUpdate();
					
					ps2.setInt(1,Integer.parseInt(textField.getText()));
					ps2.setString(2,textField_1.getText());
					ps2.setInt(3,0);
					ps2.setDouble(4,0);
					ps2.setDouble(5,Double.parseDouble(textField_3.getText()));
					ps2.executeUpdate();
					
					ps3.setInt(1,Integer.parseInt(textField.getText()));
					ps3.setString(2,textField_1.getText());
					ps3.setInt(3,0);
					ps3.setDouble(4,0);
					ps3.setDouble(5,Double.parseDouble(textField_3.getText()));
					ps3.executeUpdate();
					
					ps4.setInt(1,Integer.parseInt(textField.getText()));
					ps4.setString(2,textField_1.getText());
					ps4.setInt(3,0);
					ps4.setDouble(4,0);
					ps4.setDouble(5,Double.parseDouble(textField_3.getText()));
					ps4.executeUpdate();
					
					JOptionPane.showMessageDialog(null,"Item added Successfully !!");
					
					textField.setText("");
					textField_1.setText("");
					textField_2.setText("");
					textField_3.setText("");
					
		    	}
				catch(Exception e6)
				{
					JOptionPane.showMessageDialog(null,e6);
				}
			  }
			}
		});
		btnAddNewProduct.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnAddNewProduct.setBounds(188, 286, 199, 39);
		newproduct.add(btnAddNewProduct);
		
		JLabel lblAddingNewProduct = new JLabel("ADDING NEW PRODUCT");
		lblAddingNewProduct.setFont(new Font("Supercell-Magic", Font.BOLD, 15));
		lblAddingNewProduct.setBounds(188, 11, 262, 36);
		newproduct.add(lblAddingNewProduct);
		
		JButton btnGoBack_2 = new JButton("GO BACK");
		btnGoBack_2.setForeground(Color.WHITE);
		btnGoBack_2.setBackground(Color.BLUE);
		btnGoBack_2.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(true);
				newproduct.setVisible(false);
				textField.setText("");
				textField_1.setText("");
				textField_2.setText("");
				textField_3.setText("");
			}
		});
		btnGoBack_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_2.setBounds(186, 341, 123, 39);
		newproduct.add(btnGoBack_2);
		
		JButton btnNewButton_5 = new JButton("ADD NEW ITEM");
		btnNewButton_5.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(false);
				newproduct.setVisible(true);
		      
			}
		});
		btnNewButton_5.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_5.setBounds(220, 200, 231, 39);
		stockpage.add(btnNewButton_5);
		
		JPanel updatestock = new JPanel();
		frame.getContentPane().add(updatestock, "name_882120967973940");
		updatestock.setLayout(null);
		
		JLabel lblStockUpdate = new JLabel("STOCK  UPDATE ");
		lblStockUpdate.setFont(new Font("Supercell-Magic", Font.BOLD, 17));
		lblStockUpdate.setBounds(193, 25, 234, 32);
		updatestock.add(lblStockUpdate);
		
		JLabel lblProductId_1 = new JLabel("Product ID ");
		lblProductId_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblProductId_1.setBounds(44, 94, 140, 32);
		updatestock.add(lblProductId_1);
		
		JLabel lblQuantityToBe = new JLabel("Quantity to be added");
		lblQuantityToBe.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblQuantityToBe.setBounds(44, 155, 177, 32);
		updatestock.add(lblQuantityToBe);
		
		JLabel lblPrice_1 = new JLabel("Price");
		lblPrice_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblPrice_1.setBounds(44, 227, 109, 26);
		updatestock.add(lblPrice_1);
		
		text_id = new JTextField();
		text_id.setFont(new Font("Tahoma", Font.BOLD, 13));
		text_id.setBounds(266, 96, 161, 32);
		updatestock.add(text_id);
		text_id.setColumns(10);
		
		text_quantity = new JTextField();
		text_quantity.setFont(new Font("Tahoma", Font.BOLD, 13));
		text_quantity.setBounds(266, 157, 161, 32);
		updatestock.add(text_quantity);
		text_quantity.setColumns(10);
		
		text_price = new JTextField();
		text_price.setFont(new Font("Tahoma", Font.BOLD, 13));
		text_price.setBounds(266, 226, 161, 32);
		updatestock.add(text_price);
		text_price.setColumns(10);
		
		JButton btnUpdate = new JButton("UPDATE ");
		btnUpdate.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				int dbqty=0;//quantity of master stock
				int flag = 0 , flag1=0,flag2=0;
				if (((text_id.getText()).trim()).equals("") || ((text_quantity.getText()).trim()).equals("") || ((text_price.getText()).trim()).equals(""))
				{
					JOptionPane.showMessageDialog(null,"Please fill all the fields");
					flag = 1;
				}
				if(flag == 0)
				{
				try {
					String query8 = "SELECT master_stock FROM stock WHERE item_id=?";
					PreparedStatement pst = conn4.prepareStatement(query8);
					pst.setInt(1,Integer.parseInt(text_id.getText()));
					ResultSet rs = pst.executeQuery();
					while(rs.next())
					{
					dbqty = rs.getInt("master_stock");
					}
				}
				catch(Exception e9)
				{
					JOptionPane.showMessageDialog(null,e9);
				}
				int test = Integer.parseInt((text_quantity.getText()).trim());
				if(test > dbqty && dbqty != 0)
				{
					JOptionPane.showMessageDialog(null,"Available master stock is "+dbqty+" enter less than that");
					flag1 = 1 ;
				}
				if(dbqty==0)
				{
					int ck=0;
					try {	
					String qrryy = "SELECT * FROM items";
					PreparedStatement pd = conn1.prepareStatement(qrryy);
					ResultSet check = pd.executeQuery();
					while(check.next())
					{
					int check_id = check.getInt("item_id");
					if(check_id == Integer.parseInt(text_id.getText()))
						{
							ck=1;
						}
					}
					}catch(Exception e0)
					{
						JOptionPane.showMessageDialog(null,e0);
					}
					if(ck==1)
					{
					JOptionPane.showMessageDialog(null,"Master stock Empty !!");
					}
					else {
						JOptionPane.showMessageDialog(null,"Enter correct Item ID");
					}
					flag2=1;
				}
			}
				if(flag == 0 && flag1==0 && flag2==0)
			 {
				try {
					int updqty,updstockqty;
					updstockqty = dbqty - Integer.parseInt(text_quantity.getText()); 
				String qryy = "SELECT quantity FROM items WHERE item_id=?";
				String query3 = "UPDATE items SET quantity=?,price=? WHERE item_id=?";
				String query5 = "UPDATE stock SET master_stock=?,master_price=? WHERE item_id=?";
				String query6 = "UPDATE items SET price=? WHERE item_id=?";
				PreparedStatement ps2 = null;
				PreparedStatement ps3 = null;
				PreparedStatement ps1 = conn4.prepareStatement(query5);
				ps1.setInt(1,updstockqty);
				ps1.setInt(2,Integer.parseInt(text_quantity.getText()));
				ps1.setInt(3,Integer.parseInt(text_id.getText()));
				ps1.executeUpdate();
				if(selected_branch=="Branch 1")
				{
					ps2 = conn1.prepareStatement(qryy);
					ps3 = conn1.prepareStatement(query3);
				}
				else if(selected_branch=="Branch 2")
				{
					ps2 = conn2.prepareStatement(qryy);
					ps3 = conn2.prepareStatement(query3);
				}
				else
				{
					ps2 = conn3.prepareStatement(qryy);
					ps3 = conn3.prepareStatement(query3);
				}
				ps2.setInt(1,Integer.parseInt(text_id.getText()));
				ResultSet rs7 = ps2.executeQuery();
				while(rs7.next())
				{
				databaseqty = rs7.getInt("quantity");
				}
				updqty = databaseqty + Integer.parseInt(text_quantity.getText());
				ps3.setInt(1,updqty);
				ps3.setFloat(2,Float.parseFloat(text_price.getText()));
				ps3.setInt(3,Integer.parseInt(text_id.getText()));
				ps3.executeUpdate();
				
				PreparedStatement ps5 = conn4.prepareStatement(query5);
				ps5.setInt(1,updstockqty);
				ps5.setFloat(2,Float.parseFloat(text_price.getText()) );
				ps5.setInt(3,Integer.parseInt(text_id.getText()));
				ps5.executeUpdate();
				
				PreparedStatement pst1 = conn1.prepareStatement(query6);
				PreparedStatement pst2 = conn2.prepareStatement(query6);
				PreparedStatement pst3 = conn3.prepareStatement(query6);
				
				pst1.setFloat(1,Float.parseFloat(text_price.getText()));
				pst1.setInt(2,Integer.parseInt(text_id.getText()));
				pst1.executeUpdate();
				
				pst2.setFloat(1,Float.parseFloat(text_price.getText()));
				pst2.setInt(2,Integer.parseInt(text_id.getText()));
				pst2.executeUpdate();
				
				pst3.setFloat(1,Float.parseFloat(text_price.getText()));
				pst3.setInt(2,Integer.parseInt(text_id.getText()));
				pst3.executeUpdate();
				
				JOptionPane.showMessageDialog(null,"Updated sucessfully !! for "+selected_branch+"");
				text_id.setText("");
				text_price.setText("");
				text_quantity.setText("");
				}
				catch(Exception e6)
				{
					JOptionPane.showMessageDialog(null,e6);
				}
			 }
			}
		});
		btnUpdate.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnUpdate.setBounds(265, 295, 120, 32);
		updatestock.add(btnUpdate);
		
		JButton btnGoBack_3 = new JButton("GO BACK");
		btnGoBack_3.setForeground(Color.WHITE);
		btnGoBack_3.setBackground(Color.BLUE);
		btnGoBack_3.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				stockpage.setVisible(true);
				updatestock.setVisible(false);
				text_id.setText("");
				text_quantity.setText("");
				text_price.setText("");
			}
		});
		btnGoBack_3.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_3.setBounds(266, 350, 120, 32);
		updatestock.add(btnGoBack_3);
	
		JButton btnNewButton_4 = new JButton("UPDATE STOCK\r\n");
		btnNewButton_4.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(false);
				updatestock.setVisible(true);
			}
		});
		btnNewButton_4.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_4.setBounds(220, 94, 231, 39);
		stockpage.add(btnNewButton_4);
		
		JPanel masterstockupdate = new JPanel();
		frame.getContentPane().add(masterstockupdate, "name_892629365042476");
		masterstockupdate.setLayout(null);
		
		JLabel lblMasterStockUpdate = new JLabel("Master Stock Update");
		lblMasterStockUpdate.setFont(new Font("Supercell-Magic", Font.BOLD, 16));
		lblMasterStockUpdate.setBounds(179, 11, 297, 32);
		masterstockupdate.add(lblMasterStockUpdate);
		
		JLabel lblProductId_2 = new JLabel("Product ID");
		lblProductId_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblProductId_2.setBounds(51, 88, 149, 32);
		masterstockupdate.add(lblProductId_2);
		
		JLabel lblQuantity_1 = new JLabel("Quantity");
		lblQuantity_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblQuantity_1.setBounds(51, 153, 147, 32);
		masterstockupdate.add(lblQuantity_1);
		
		JLabel lblPrice_2 = new JLabel("Price");
		lblPrice_2.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblPrice_2.setBounds(51, 221, 149, 32);
		masterstockupdate.add(lblPrice_2);
		
		textField_4 = new JTextField();
		textField_4.setFont(new Font("Tahoma", Font.BOLD, 14));
		textField_4.setBounds(201, 90, 160, 32);
		masterstockupdate.add(textField_4);
		textField_4.setColumns(10);
		
		textField_5 = new JTextField();
		textField_5.setFont(new Font("Tahoma", Font.BOLD, 14));
		textField_5.setBounds(201, 155, 160, 32);
		masterstockupdate.add(textField_5);
		textField_5.setColumns(10);
		
		textField_6 = new JTextField();
		textField_6.setFont(new Font("Tahoma", Font.BOLD, 14));
		textField_6.setBounds(202, 223, 160, 32);
		masterstockupdate.add(textField_6);
		textField_6.setColumns(10);
		
		JButton btnUpdate_1 = new JButton("UPDATE");
		btnUpdate_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					int flag = 0;
					int dbqty=0,updateqty=0;
					int flag1=0;
					if(textField_4.getText().equals("") || textField_5.getText().equals("") || textField_6.getText().equals("") )
					{
						JOptionPane.showMessageDialog(null,"Please fill all the fields");
						flag1=1;
					}
					if(flag1==0)
					{
					String update = "SELECT master_stock FROM stock WHERE item_id=?";
					PreparedStatement pss = conn4.prepareStatement(update);
					pss.setInt(1,Integer.parseInt(textField_4.getText()));
					ResultSet rss = pss.executeQuery();
					while(rss.next())
					{
						dbqty = rss.getInt("master_stock");
						flag=1;
					}
				    updateqty = dbqty + Integer.parseInt(textField_5.getText().trim());
					}
				    if(flag==1 && flag1==0)
				    {
				    	String upd = "UPDATE stock SET master_stock=?,master_price=? WHERE item_id=?";
				    	String price = "UPDATE items SET price=? WHERE item_id=?";
				    	PreparedStatement pst2 = conn4.prepareStatement(upd);
				    	pst2.setInt(1,updateqty);
				    	pst2.setFloat(2,Float.parseFloat(textField_6.getText()));
				    	pst2.setInt(3,Integer.parseInt(textField_4.getText()));
				    	pst2.executeUpdate();
				    	
				    	PreparedStatement pst3 = conn1.prepareStatement(price);
				    	PreparedStatement pst4 = conn2.prepareStatement(price);
				    	PreparedStatement pst5 = conn3.prepareStatement(price);
				    	
				    	pst3.setFloat(1,Float.parseFloat(textField_6.getText()) );
				    	pst3.setInt(2,Integer.parseInt(textField_4.getText()));
				    	pst3.executeUpdate();
				    	
				    	pst4.setFloat(1,Float.parseFloat(textField_6.getText()) );
				    	pst4.setInt(2,Integer.parseInt(textField_4.getText()));
				    	pst4.executeUpdate();
				    	
				    	pst5.setFloat(1,Float.parseFloat(textField_6.getText()) );
				    	pst5.setInt(2,Integer.parseInt(textField_4.getText()));
				    	pst5.executeUpdate();
				    	JOptionPane.showMessageDialog(null,"master stock update successfull");	
				    	textField_4.setText("");
						textField_5.setText("");
						textField_6.setText("");
				    }
				    else
				    {
				    	if(flag1==0)
				    	{
				    	JOptionPane.showMessageDialog(null,"Enter correct Item ID");
				    	}
				    }
				}catch(Exception e3)
				{
				   e3.printStackTrace();
				}
				
			}
		});
		btnUpdate_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnUpdate_1.setBounds(201, 279, 137, 45);
		masterstockupdate.add(btnUpdate_1);
		
		JButton btnNewButton_6 = new JButton("GO BACK");
		btnNewButton_6.setForeground(Color.WHITE);
		btnNewButton_6.setBackground(Color.BLUE);
		btnNewButton_6.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(true);
				masterstockupdate.setVisible(false);
				textField_4.setText("");
				textField_5.setText("");
				textField_6.setText("");
			}
		});
		btnNewButton_6.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewButton_6.setBounds(199, 348, 139, 45);
		masterstockupdate.add(btnNewButton_6);
		
		JButton btnUpdateMasterStock = new JButton("UPDATE MASTER STOCK");
		btnUpdateMasterStock.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				masterstockupdate.setVisible(true);
				stockpage.setVisible(false);
			}
		});
		btnUpdateMasterStock.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnUpdateMasterStock.setBounds(220, 144, 231, 45);
		stockpage.add(btnUpdateMasterStock);
		
		JPanel masterstockdisplay = new JPanel();
		frame.getContentPane().add(masterstockdisplay, "name_893715079903732");
		masterstockdisplay.setLayout(null);
		
		JScrollPane scrollPane_2 = new JScrollPane();
		scrollPane_2.setBounds(38, 58, 563, 293);
		masterstockdisplay.add(scrollPane_2);
		
		table_2 = new JTable();
		table_2.setFont(new Font("Tahoma", Font.BOLD, 14));
		table_2.setRowSelectionAllowed(false);
		table_2.setEnabled(false);
		scrollPane_2.setViewportView(table_2);
		
		JButton btnGoBack_4 = new JButton("GO BACK");
		btnGoBack_4.setForeground(Color.WHITE);
		btnGoBack_4.setBackground(Color.BLUE);
		btnGoBack_4.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				stockpage.setVisible(true);
				masterstockdisplay.setVisible(false);
			}
		});
		btnGoBack_4.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnGoBack_4.setBounds(297, 358, 112, 35);
		masterstockdisplay.add(btnGoBack_4);
		
		JButton btnViewMasterStock = new JButton("VIEW MASTER STOCK");
		btnViewMasterStock.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				try {
					String master = "SELECT * FROM stock";
					PreparedStatement ps1 = conn4.prepareStatement(master);	
					ResultSet rs2 = ps1.executeQuery();
					table_2.setModel(DbUtils.resultSetToTableModel(rs2));	
					masterstockdisplay.setVisible(true);
					stockpage.setVisible(false);
				}catch(Exception e8)
				{
					JOptionPane.showMessageDialog(null,e8);
				}
			}
		});
		btnViewMasterStock.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnViewMasterStock.setBounds(411, 290, 210, 39);
		stockpage.add(btnViewMasterStock);
		
	}
	
	
	
}
