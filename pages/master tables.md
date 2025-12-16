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
- -----------------------------
- ----------------
-
-
- ------------------
-
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