# Relational Database Management System (RDBMS)

###### MS SQL as an example

# Directory
- [Description](#Description)
- [Structure](#Structure)
- [Commands](#Commands)
## Description
An RDBMS , such as Microsoft SQL (Structured Query Language) can be visualized as a group of tables that all have relationships. 

## Structure
Consider an online grocery store database with three tables.

1. Produce
2. Customers
3. Invoices

*Each **Produce** table has the columns*
- ID
- Name
- Price
- Quantity

*Each **Customer** table has the columns*
- ID
- Name
- Price
- Quantity

The **Invoices** table shares information from both, referring to a single customer per row with one or more produce items. This table refers to another table using its ID. In this way, we only need to have the customer details and the invoice written once instead of copying them each to a new invoice.

***For example***
###### These are two separate tables  
<table>
	<thead>
		<tr>
			<th colspan=2><b>customers</b></th>
			<th><b>...next table...</b></th>
			<th colspan=2><b>produce</b></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><b>id</b></td>
			<td><b>name</b></td>
			<td><b>...next table...</b></td>
			<td><b>id</b></td>
			<td><b>name</b></td>
		</tr>
		<tr>
			<td>101</td>
			<td>Michael</td>
			<td><b>...next table...</b></td>
			<td>1</td>
			<td>Lettuce</td>
		</tr>
		<tr>
			<td>102</td>
			<td>Katrina</td>
			<td><b>...next table...</b></td>
			<td>2</td>
			<td>Tomato</td>
		</tr>
		<tr>
			<td>103</td>
			<td>John</td>
			<td><b>...next table...</b></td>
			<td>3</td>
			<td>Banana</td>
		</tr>
	</tbody>
</table>

**Invoice**
###### Contains the `ID` from **Customer** and the `ID` from **Produce**
| id_customer | id_produce |   
| --- | --- |   
| 101 | 3, 1 |   
| 102 | 1 |   
| 103 | 2, 3 |   

## Commands
### MySQL
#### Enumerating
- `show databases;` - Shows all available databasaes