
import java.awt.*;
import javax.swing.table.*;
import java.sql.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import javax.swing.JFrame;
import java.awt.CardLayout;
import javax.swing.JPanel;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import java.awt.Font;
import javax.swing.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;


public class Billing extends LoginPage {

	private JFrame frame;
	private JTextField textitem_id;
	private JTextField textquantity;
	private JTextField textmobile;
	private JTextField textcustomer_name;
	private JPanel billingpage;
	private JLabel lblBilling;
	private JLabel lblDate;
	private JLabel lblUsername;
	private JLabel lblitem_id ;
	private JLabel lblquantity;
	private JLabel lblCustomerName;
	private JLabel lblMobileNo ;
	private JLabel lblTotalPrice;
	private JTextArea date ;
	private JTextArea username ;
	private JTextArea total;
	private JPanel displaybill = new JPanel();
	private static final DateFormat dateTime = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
	public static int globalqty;

	/**
	 * Launch the application.
	 */
	DefaultTableModel tab;
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Billing window = new Billing();
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
	private JTable table;
	private JTable table_1;
	private JButton btnNewBilling;
	private JLabel lblCustomerName_1;
	private JTextField textcustname;
	private JLabel lblGrandTotal;
	private JLabel labeltotalamount;
	private JLabel lblThanks;
	public Billing() {
		initialize();

	}
	//function for creating column
	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		
		//connecting with database 
		frame = new JFrame();
		frame.setBounds(100, 100, 773, 519);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(new CardLayout(0, 0));
		
		billingpage= new JPanel();
		frame.getContentPane().add(billingpage, "name_451140683030028");
	    billingpage.setLayout(null);
		
	    lblBilling = new JLabel("BILLING");
	    lblBilling.setBounds(321, 11, 194, 25);
		lblBilling.setFont(new Font("Supercell-Magic", Font.BOLD, 20));
		billingpage.add(lblBilling);
		
		lblDate = new JLabel("Date");
		lblDate.setBounds(10, 52, 90, 25);
		lblDate.setFont(new Font("Supercell-Magic", Font.BOLD, 15));
		billingpage.add(lblDate);
		
	    lblUsername = new JLabel("Username");
	    lblUsername.setBounds(10, 93, 122, 25);
		lblUsername.setFont(new Font("Supercell-Magic", Font.BOLD, 15));
		billingpage.add(lblUsername);
		
		JButton btnLogOut = new JButton("LOG OUT");

		btnLogOut.setBounds(394, 71, 132, 31);
		btnLogOut.setBackground(Color.RED);
		btnLogOut.setForeground(Color.WHITE);
		btnLogOut.setFont(new Font("Supercell-Magic", Font.BOLD, 15));
		billingpage.add(btnLogOut);
		
	    lblitem_id = new JLabel("Item ID");
	    lblitem_id.setBounds(475, 234, 74, 25);
		lblitem_id.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(lblitem_id);
		
	    lblquantity = new JLabel("Quantity");
	    lblquantity.setBounds(475, 284, 74, 25);
		lblquantity.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(lblquantity);
		
		textitem_id = new JTextField();
		textitem_id.setBounds(602, 236, 132, 25);
		billingpage.add(textitem_id);
		textitem_id.setColumns(10);
		
		textquantity = new JTextField();
		textquantity.setBounds(602, 286, 132, 25);
		billingpage.add(textquantity);
		textquantity.setColumns(10);
		
		JButton btnAdd = new JButton("ADD");
		btnAdd.setBounds(602, 331, 116, 31);
		btnAdd.setBackground(Color.GRAY);
		btnAdd.setForeground(Color.GREEN);
		btnAdd.setFont(new Font("Tahoma", Font.BOLD, 15));
		//table columns
		table = new JTable();
		table.setFont(new Font("Tahoma", Font.BOLD, 11));
		Object[] columns = {"ITEM ID","ITEM NAME","QUANTITY","PRICE"};
		DefaultTableModel model = new DefaultTableModel();
		model.setColumnIdentifiers(columns);
		table.setModel(model);
		JScrollPane scrollPane = new JScrollPane();
		scrollPane.setBounds(20, 142, 445, 252);
		billingpage.add(scrollPane);
		
		table.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
		scrollPane.setViewportView(table);
		
		Object[] row = new Object[4];
		btnAdd.addActionListener(new ActionListener() 
		{
			public void actionPerformed(ActionEvent e) 
			{
				textitem_id.setEditable(true);
				//Add button performed
				int id=0,qty=0;
				int dbqty;
				String checkid = textitem_id.getText();
				String checkqty = textquantity.getText();
				String cname = textcustomer_name.getText();
				String no = textmobile.getText();
				String dbitemname=null;
				float dbprice=0;
				float totprice=0;
				int flag=0,flag1=0,flag2=0,dbquantity=0;
				if (cname.equals("") || no.equals("") || checkid.equals("") || checkqty.equals("") )
				{
					flag=1;
					JOptionPane.showMessageDialog(null,"Please fill all the details");
				}
				//integer parsing should be given in try catch block else java.lang.numberexception error will be displayed
				if(flag==0)
				{
				try {
			     id = Integer.parseInt(textitem_id.getText());
				 qty = Integer.parseInt(textquantity.getText());
				}
				catch(Exception e5)
				{
					JOptionPane.showMessageDialog(null,e5);
				}
				Statement st1 = null;
				Statement st2 = null;
				Statement st3 = null;
				//Statement will not work without try catch block
				int count=0,count1=0;
				//statement creating line will be an error without try catch block
				try {
					st1 = conn1.createStatement();
					st2 = conn2.createStatement();
					st3 = conn3.createStatement();
				} catch (SQLException e1)
				{
					JOptionPane.showMessageDialog(null,e);
				}
				String query1 = "SELECT quantity FROM items where item_id ='"+id+"'";
				String query2 = "SELECT item_name FROM items where item_id ='"+id+"'";
				String query3 = "SELECT price FROM items where item_id ='"+id+"'";
				
				try 
				{
					ResultSet rs1 = null;
					if(selected_branch=="Branch 1")
					{
				      rs1= st1.executeQuery(query1);
					}else if (selected_branch=="Branch 2")
					{
						  rs1= st2.executeQuery(query1);
					}
					else
					{
						 rs1= st3.executeQuery(query1);
					}				
				while(rs1.next())
				{
					count++;
				     dbqty = rs1.getInt("quantity");
				     dbquantity = dbqty;
				     if(dbqty==0)
				     {
				    	 flag2=1;
				    	 JOptionPane.showMessageDialog(null,"Stock Empty!!");
				    	 textitem_id.setText("");
				    	 textquantity.setText("");
				     }
					if (qty > dbqty && flag2==0)
					{
						 flag1=1;
						JOptionPane.showMessageDialog(null,"Available Stock is "+dbqty+" please enter less than that");
					}
				}
				ResultSet rs2 = null;
				if(selected_branch=="Branch 1")
				{
				 rs2 = st1.executeQuery(query2);
				}
				else if(selected_branch=="Branch 2")
				{
				 rs2 = st2.executeQuery(query2);
				}
				else
				{
				 rs2 = st3.executeQuery(query2);
				}
				while(rs2.next())
				{
					count1++;
					 dbitemname = rs2.getString("item_name");
				}
				ResultSet rs3 = null;
				if (selected_branch=="Branch 1")
				{
			    rs3 = st1.executeQuery(query3);
				}
				else if (selected_branch=="Branch 2")
				{
			    rs3 = st2.executeQuery(query3);
				}
				else
				{
			    rs3 = st3.executeQuery(query3);
				}
				while(rs3.next())
				{
					dbprice = rs3.getFloat("price");
				}
			    if(count==0 || count1==0)
			    {
			    	if(flag!=1)
			    	{
			    	JOptionPane.showMessageDialog(null,"Please Enter correct Item ID");
			    	}
			    }
				}
				catch(Exception e2)
				{
					JOptionPane.showMessageDialog(null,e2);
				}
				//calculating total price
				totprice = qty*dbprice;	
			    if(count!=0 && count1!=0 && flag!=1 && flag1!=1 && flag2!=1)
			    {   
			    	row[0] =  id ;
					row[1] =  dbitemname;
				    row[2] =  qty;
				    row[3] =  totprice;
			        model.addRow(row);
			        textitem_id.setText("");
			        textquantity.setText("");
			        dbquantity=dbquantity-qty;
			        try {
			        	PreparedStatement ps1 =null;
			        	String update_query = "UPDATE items SET quantity=? WHERE item_id=?";
			        	if (selected_branch=="Branch 1")
			        	{
						ps1 = conn1.prepareStatement(update_query);
			        	}
			        	else if (selected_branch=="Branch 2")
			        	{
						ps1 = conn2.prepareStatement(update_query);
			        	}
			        	else
			        	{
						ps1 = conn3.prepareStatement(update_query);
			        	}
						ps1.setInt(1,dbquantity);
						ps1.setInt(2,id);
						ps1.executeUpdate();
					} catch (SQLException e1) 
			        {
						JOptionPane.showMessageDialog(null,e1);
					}
			    }
			    //displaying total
			    int no_of_rows = table.getRowCount();
			    double sum =0;
			    for(int j=0;j<no_of_rows;j++)
			    {
			    	String curr_price = model.getValueAt(j,3).toString();
			    	double currentprice= Double.parseDouble(curr_price);
			    	sum = sum + currentprice;
			    }
			    total.setText(String.valueOf(sum));
			    total.setEditable(false);
				} 
			}
		});
		
		table.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseClicked(MouseEvent arg0) {
				int i = table.getSelectedRow();//i is the row number 
				textitem_id.setText(model.getValueAt(i, 0).toString());
				textquantity.setText(model.getValueAt(i, 2).toString());
				try {
					globalqty=Integer.parseInt(model.getValueAt(i,2).toString());
					//java.lang.classcastException ...object type casting to int problem ..use Integer.parse
				}
				catch(Exception e)
				{
					JOptionPane.showMessageDialog(null,e);
				}
				textitem_id.setEditable(false);
			}
		});
		
		
		billingpage.add(btnAdd);
		
		JButton btnRemove = new JButton("REMOVE");
		btnRemove.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				textitem_id.setEditable(true);
				int i = table.getSelectedRow();
				int flag = 0;
				if(i>=0)
				{
					model.removeRow(i);
				}
				else
				{
					flag = 1;
					JOptionPane.showMessageDialog(null,"Table is empty");
				}
				if(flag == 0)
				{
				 try {
					    int id =Integer.parseInt(textitem_id.getText());
				        int qty=Integer.parseInt(textquantity.getText());
				    	int dbquantity=0;
				    	String query = "SELECT quantity FROM items WHERE item_id='"+id+"'";
				    	String update_query = "UPDATE items SET quantity=? WHERE item_id=?";
						Statement st1 = null;
						PreparedStatement ps1 = null;
						ResultSet rs = null;
						if(selected_branch=="Branch 1")
						{
							 st1 = conn1.createStatement();
							 ps1 = conn1.prepareStatement(update_query);
						   
						}
						else if(selected_branch=="Branch 2")
						{
							 st1 = conn2.createStatement();
							 ps1 = conn2.prepareStatement(update_query);
						   
						}
						else
						{
							 st1 = conn3.createStatement();
							 ps1 = conn3.prepareStatement(update_query);
						   
						}
						 rs = st1.executeQuery(query);
						//Don't forget to use while loop. if not error is SQLexception...
						while(rs.next())
						{
						dbquantity = rs.getInt("quantity");
						}
						dbquantity = dbquantity+qty;
						ps1.setInt(1,dbquantity);
						ps1.setInt(2,id);
						ps1.executeUpdate();		
					} catch (SQLException e) 
				 {
					 JOptionPane.showMessageDialog(null,e);
				 }

				textitem_id.setText("");
				textquantity.setText("");
				//Displaying total
				  int no_of_rows = table.getRowCount();
				    double sum =0;
				    for(int j=0;j<no_of_rows;j++)
				    {
				    	String curr_price = model.getValueAt(j,3).toString();
				    	double currentprice= Double.parseDouble(curr_price);
				    	sum = sum + currentprice;
				    }
				    total.setText(String.valueOf(sum));
				    total.setEditable(false);
				    //for dyanamic changing of quantity value
				}  
			}
			
		});
		btnRemove.setBounds(602, 373, 116, 31);
		btnRemove.setForeground(Color.RED);
		btnRemove.setBackground(Color.GRAY);
		btnRemove.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(btnRemove);
		
		JButton btnUpdate = new JButton("UPDATE");
		btnUpdate.setBounds(602, 415, 116, 31);
		btnUpdate.setForeground(Color.WHITE);
		btnUpdate.setBackground(Color.GRAY);
		btnUpdate.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnUpdate.addActionListener(new ActionListener() {
			//update action performed
			public void actionPerformed(ActionEvent e) {
				int flag=0;
				String idcheck = textitem_id.getText();
				String qtycheck = textquantity.getText();
				float dbprice=0;
				int dbqty=0;
				float updateprice=0;
				String query1 = "SELECT price FROM items WHERE item_id='"+idcheck+"'";
				String query2 = "SELECT quantity FROM items WHERE item_id='"+idcheck+"'";
				if(idcheck.equals("")|| qtycheck.equals(""))
				{
					flag=1;
					JOptionPane.showMessageDialog(null,"Cannot update with Empty fields");
				}
				try {
					Statement s1 = null;
					Statement s2 = null;
					if(selected_branch=="Branch 1")
	             	{
							s1 =conn1.createStatement();
							s2 =conn1.createStatement();
	            	}
					else if(selected_branch=="Branch 2")
	             	{
							s1 =conn2.createStatement();
							s2 =conn2.createStatement();
	            	}
					else
	             	{
							s1 =conn3.createStatement();
							s2 =conn3.createStatement();
	            	}
					ResultSet rs1 = s1.executeQuery(query1);
					ResultSet rs2 = s2.executeQuery(query2);
					while(rs1.next())
					{
					dbprice = rs1.getFloat("price");
					}
					while(rs2.next())
					{
					dbqty = rs2.getInt("quantity");
					}
				} catch (SQLException e1) {
					JOptionPane.showMessageDialog(null,e1);
				}				
				if(flag == 0)
				{
				updateprice = Integer.parseInt(qtycheck)*dbprice;
				int i = table.getSelectedRow();
				if(i>=0)
				{	
					if(Integer.parseInt(qtycheck)<=dbqty || (dbqty==0 && Integer.parseInt(qtycheck)<=globalqty))
					{
					model.setValueAt(textquantity.getText(), i, 2);
					model.setValueAt(updateprice,i,3);
					int updatedbqty = dbqty+globalqty-Integer.parseInt(qtycheck);
					String updatequery= "UPDATE items SET quantity=? WHERE item_id=?";
					try {
						PreparedStatement ps1 = null;
						if(selected_branch=="Branch 1")
						{
								ps1 = conn1.prepareStatement(updatequery);
						}
						else if(selected_branch=="Branch 2")
						{
								ps1 = conn2.prepareStatement(updatequery);
						}
						else
						{
								ps1 = conn3.prepareStatement(updatequery);
						}
						ps1.setInt(1,updatedbqty);
						ps1.setInt(2,Integer.parseInt(idcheck));
						ps1.executeUpdate();
					} catch (SQLException e1) {
						JOptionPane.showMessageDialog(null,e1);
					}
					}
					else
					{
						if(dbqty==0 && Integer.parseInt(qtycheck)>globalqty)
						{
							JOptionPane.showMessageDialog(null,"Stock Empty !!");
						}
						else {
							
						JOptionPane.showMessageDialog(null,"Available stock is "+dbqty+" Please enter less than that");
						}
					}
				}
				else
				{
					JOptionPane.showMessageDialog(null,"Table is Empty");
				}
				textitem_id.setText("");
		        textquantity.setText("");
		        textitem_id.setEditable(true);
		        //Displaying total
		        int no_of_rows = table.getRowCount();
			    double sum =0;
			    for(int j=0;j<no_of_rows;j++)
			    {
			    	String curr_price = model.getValueAt(j,3).toString();
			    	double currentprice= Double.parseDouble(curr_price);
			    	sum = sum + currentprice;
			    }
			    total.setText(String.valueOf(sum));
			    total.setEditable(false);
			  }
				
			}
		});
		billingpage.add(btnUpdate);
		
	    lblCustomerName = new JLabel("Customer name");
	    lblCustomerName.setBounds(470, 126, 116, 42);
		lblCustomerName.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(lblCustomerName);
		
	    lblMobileNo = new JLabel("Mobile no");
	    lblMobileNo.setBounds(470, 179, 95, 25);
		lblMobileNo.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(lblMobileNo);
		
		textmobile = new JTextField();
		textmobile.setBounds(602, 183, 132, 27);
		billingpage.add(textmobile);
		textmobile.setColumns(10);
		
		textcustomer_name = new JTextField();
		textcustomer_name.setBounds(602, 135, 132, 25);
		billingpage.add(textcustomer_name);
		textcustomer_name.setColumns(10);
		
		JButton btnGenerateBill = new JButton("GENERATE BILL");
		btnGenerateBill.setBounds(292, 409, 170, 42);
		btnGenerateBill.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				String cname = textcustomer_name.getText();
				String no = textmobile.getText();
				int no_of_rows = table.getRowCount();
				int col1=0,col3=0;
				float col4=0;
				String query1= "INSERT INTO customer_details(name,phone_no,item_id,quantity,price) VALUES (?,?,?,?,?)";
				try 
				{
					PreparedStatement st1 = null;
					if (selected_branch=="Branch 1")
					{
							st1 =conn1.prepareStatement(query1);
					}
					else if (selected_branch=="Branch 2")
					{
							st1 =conn2.prepareStatement(query1);
					}
					else
					{
							st1 =conn3.prepareStatement(query1);
					}
					for(int i=0;i<no_of_rows;i++)
					{
					col1=Integer.parseInt(table.getValueAt(i,0).toString());
					col3=Integer.parseInt(table.getValueAt(i,2).toString());
					col4=Float.parseFloat(table.getValueAt(i,3).toString());
					//col3 = (int)table.getValueAt(i,2); this type of casting will lead to java.lang.ClassCastException:
					st1.setString(1,cname);
					st1.setString(2,no);
					st1.setInt(3,col1);
					st1.setInt(4,col3);
					st1.setFloat(5,col4);
					st1.executeUpdate();
					}
				} catch (SQLException e1)
				{
					JOptionPane.showMessageDialog(null,e1);
				}
				billingpage.setVisible(false);
				lblGrandTotal.setVisible(false);
				labeltotalamount.setVisible(false);
				lblThanks.setVisible(false);
				displaybill.setVisible(true);
				textcustname.setText("");
				labeltotalamount.setText("");
				DefaultTableModel dm1 = (DefaultTableModel)table_1.getModel();
				while(dm1.getRowCount() > 0)
				{
				    dm1.removeRow(0);
				}
			}
		});
		btnGenerateBill.setBackground(Color.BLUE);
		btnGenerateBill.setForeground(Color.WHITE);
		btnGenerateBill.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(btnGenerateBill);
		
	    lblTotalPrice = new JLabel(" TOTAL PRICE :");
	    lblTotalPrice.setForeground(Color.BLACK);
	    lblTotalPrice.setBounds(20, 415, 116, 31);
		lblTotalPrice.setFont(new Font("Tahoma", Font.BOLD, 15));
		billingpage.add(lblTotalPrice);
		
	    date = new JTextArea();
	    date.setBounds(132, 55, 166, 30);
		date.setFont(new Font("Monospaced", Font.BOLD, 13));
		date.setEditable(false);
		billingpage.add(date);
		
	    username = new JTextArea();
	    username.setFont(new Font("Monospaced", Font.BOLD, 15));
	    username.setBounds(132, 96, 166, 25);
		username.setEditable(false);
		billingpage.add(username);
		
		username.setText(usrname);
		
		
	    total= new JTextArea();
	    total.setFont(new Font("Tahoma", Font.BOLD, 17));
	    total.setBounds(146, 420, 132, 26);
		total.setEditable(false);
		billingpage.add(total);
		
		
		frame.getContentPane().add(displaybill, "name_451157147657656");
		displaybill.setLayout(null);
		
		
		JScrollPane scrollPane_1 = new JScrollPane();
		scrollPane_1.setEnabled(false);
		scrollPane_1.setBounds(63, 128, 517, 279);
		displaybill.add(scrollPane_1);
		
		table_1 = new JTable();
		table_1.setRowSelectionAllowed(false);
		table_1.setEnabled(false);
		table_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		scrollPane_1.setViewportView(table_1);
		DefaultTableModel model1 = new DefaultTableModel();
		
		JButton btnDisplayBill = new JButton("DISPLAY BILL");
		btnDisplayBill.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnDisplayBill.setBounds(428, 86, 152, 39);
		displaybill.add(btnDisplayBill);
		
		Object billcolumn[] = {"ITEM ID","ITEM NAME","QUANTITY","PRICE"};
		model1.setColumnIdentifiers(billcolumn);
		table_1.setModel(model1);
		
		lblGrandTotal = new JLabel("GRAND TOTAL :");
		lblGrandTotal.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblGrandTotal.setBounds(63, 418, 132, 31);
		displaybill.add(lblGrandTotal);
		
	    labeltotalamount = new JLabel("");
		labeltotalamount.setFont(new Font("Tahoma", Font.BOLD, 15));
		labeltotalamount.setBounds(194, 418, 112, 31);
		displaybill.add(labeltotalamount);	

	    lblThanks = new JLabel("Thanks for shopping with us .Visit again !!!");
		lblThanks.setFont(new Font("Supercell-Magic", Font.BOLD, 15));
		lblThanks.setBounds(118, 11, 526, 36);
		displaybill.add(lblThanks);
		
		btnNewBilling = new JButton("NEW BILLING");
		btnNewBilling.setForeground(Color.WHITE);
		btnNewBilling.setBackground(Color.BLUE);
		btnNewBilling.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				textcustomer_name.setText("");
				textmobile.setText("");
				textitem_id.setText("");
				textquantity.setText("");
				total.setText("");
				textitem_id.setEditable(true);
				DefaultTableModel dm = (DefaultTableModel)table.getModel();
				while(dm.getRowCount() > 0)
				{
				    dm.removeRow(0);
				}
				displaybill.setVisible(false);				
				billingpage.setVisible(true);
			}
		});
		btnNewBilling.setFont(new Font("Tahoma", Font.BOLD, 15));
		btnNewBilling.setBounds(420, 414, 160, 39);
		displaybill.add(btnNewBilling);
		
		lblCustomerName_1 = new JLabel("CUSTOMER NAME :");
		lblCustomerName_1.setFont(new Font("Tahoma", Font.BOLD, 15));
		lblCustomerName_1.setBounds(62, 93, 142, 24);
		displaybill.add(lblCustomerName_1);
		
		textcustname = new JTextField();
		textcustname.setFont(new Font("Tahoma", Font.BOLD, 15));
		textcustname.setEditable(false);
		textcustname.setBounds(220, 89, 198, 31);
		displaybill.add(textcustname);
		textcustname.setColumns(10);
		Object[] billrow = new Object[4];
		
		btnDisplayBill.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
			int tablerows = table.getRowCount();
			int i = 0;
			for(i=0;i<tablerows;i++)
			  {
				billrow[0] = table.getValueAt(i,0);
				billrow[1] = table.getValueAt(i,1);
				billrow[2] = table.getValueAt(i,2);
				billrow[3] = table.getValueAt(i,3);
				model1.addRow(billrow);
			  }
			textcustname.setText(textcustomer_name.getText());
			labeltotalamount.setText(total.getText());
			if((textcustname.getText().equals(""))==false)
			 {
			lblGrandTotal.setVisible(true);
			labeltotalamount.setVisible(true);
			lblThanks.setVisible(true);	
			 }
			}
		});
		
		//for date and time
		Calendar cal = Calendar.getInstance();
		date.setText(dateTime.format(cal.getTime()));
		
		btnLogOut.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				try {
					String query ="INSERT INTO loginDetails(username,logintime,logout_time)VALUES(?,?,?)";
					PreparedStatement ps1 = conn4.prepareStatement(query);
					ps1.setString(1,usrname);
					ps1.setString(2,dateandtime);
					ps1.setString(3,date.getText());
					ps1.executeUpdate();	
				} catch (SQLException e) {
					JOptionPane.showMessageDialog(null,e);
				}
				frame.dispose();
				LoginPage.main(null);
			}
		});
	
	}
}
