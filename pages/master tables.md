- Customer Master Tables (pure customer)
  title:: master tables
	- CBS.STTM_CUSTOMER (**customer_no**)
		- customer_type
			- Indicates whether the customer is Individual (‘I’) or Corporate (‘C’), Bank (‘B’)
		- record_status
			- Record status (O – Open, C – Closed)
	- CBS.STTM_CUST_PERSONAL (**customer_no**)
		- date_of_birth
		- sex
		- telephone
		- mobile_number
- ------------
- Customer Master Link Table or Master Table (pure customer)
	- CBS.STTM_CUST_ACCOUNT (cust_ac_no,cust_no)
	- ```sql
	  KBZ Bank Account has 17 digits. (e.g 02130102145833301)
	  	1-3 = account branch code
	  	4-6 = account class/type
	  	7-15 = CIF (customer ID)
	  	16-17 = number of accounts
	  If first prefix number of account class is
	  	1 --> Current
	  	2 --> Nostro
	  	3 --> Saving
	  	4 --> Fixed
	  	5 --> Call
	  	6 --> Overdraft
	  	7 --> Integrated Liquidity Management
	  	8 --> Trust/Current Converted
	  
	  ```
- -----------------------------
- Branch Master
	- ~~CBS.STTM_BRANCH~~
	  background-color:: gray
	- ```sql
	  select * from CBS.STTM_BRANCH where branch_code <= '021' order by branch_code
	  ```
	- ~~but it is not used because this is raw~~
	-
	- dimension.cbs_branch (used)
		- branch_status (open , closed)
		- head_count
		- territory (Branch Operations) eg. Yangon,Naypyitaw and Lower Myanmar
		- ri_name (Regional In-Charge Name) eg. Daw Khet Khet Nwe
		- head_of_ri_name (Head of Regional In-Charge) eg. U Tin Win
		- tc_branch_status (Operational status of the branch to be considered for TC) eg. Open, Closed
- ----------------
- Account Class or Product Master
	- ~~CBS.STTM_ACCOUNT_CLASS~~
		- ~~account_class (code)~~
		- ~~description (product name)~~
-
	- dimension.cbs_acc_class (use this instead of ~~CBS.STTM_ACCOUNT_CLASS~~)
		- lookup.cbs_acc_class +
		- cbs.sttm_account_class(unknow source) +
		- lookup.cbs_acc_class_dbu_csv (csv)
			- ```sql
			  acc_clas
			  acc_desc
			  acc_category
			  classification_group
			  classification_finance
			  classification_deposit
			  deposit_flag
			  ```
	- -------------
- CBS.GLTM_GLMASTER (not include balance , use for mapping only)
	- this table is use for gl mapping with parent_gl and desc
		- ```sql
		  gl_code
		  gl_desc
		  parent_gl
		  ```
-
- ------------------
-
- ParaTable (config table)
	- this table is use for gl posting d or c by account_class and status
		- CBS.STTM_ACCOUNT_CLASS_STATUS
			- ```sql
			  account_class
			  status
			  dr_gl
			  cr_gl
			  ```
- -------------
-
- TranCode Table
	- this table is use for transaction classification which trancode is use for.
		- CBS.STTM_TRN_CODE
			- ```sql
			  account_class (code)
			  status (code detail)
			  dr_gl
			  cr_gl
			  ```
-
- -----------------
- account_class and product understanding
  background-color:: blue
	- there are 4 types of table
	  background-color:: blue
		- CBS.STTM_ACCOUNT_CLASS_STATUS (config table)
		  background-color:: blue
		- dimension.cbs_acc_class (dbt model)
		  background-color:: blue
		- CBS.CSTM_PRODUCT (detail product classification)
		  background-color:: blue
		- LOOKUP.CBS_PRODUCT (function code that can be match with product_code)
		  background-color:: blue
		- background-color:: blue
	- remark - function code is more detail than product_code
	  background-color:: blue
	- background-color:: blue
	- remark - you can define a product by 3 type.
	  background-color:: blue
		- account class (config)
		  background-color:: blue
		- product (operation useage)
		  background-color:: blue
		- function code
		  background-color:: blue
- ------
- CBS.CSTM_PRODUCT (operation useage)
	- this table store financial products and services offered by the bank
		- ```sql
		  product_code
		  product_description
		  ```
-
- ---------
- LOOKUP.CBS_PRODUCT
	- keeps mapping between product and function code
		- ```sql
		  product
		  product_desc
		  function_code
		  ```
-
- -------------------
- CBS.STTM_AC_LINKED_ENTITIES
	- joint account and joint customer
		- ```sql
		  cust_ac_no
		  joint_holder_code
		  ```
-
- ---------
-
-
-
-
-
-
-