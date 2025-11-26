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
-
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
			-
- CBS.GLTM_GLMASTER (not include balance , use for mapping only)
	-
	- ```sql
	  gl_code
	  gl_desc
	  parent_gl
	  ```
-
- ParaTable
	- this table is use for gl posting d or c by account_class and status
		- CBS.STTM_ACCOUNT_CLASS_STATUS
			- ```sql
			  account_class
			  status
			  
			  ```
			-
- TranCode Table
	- this table is use for transaction classification which trancode is use for.
		- CBS.STTM_TRN_CODE
	-