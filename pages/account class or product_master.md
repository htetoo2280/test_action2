- Account Class or Product Master
  title:: account class or product_master
	- ~~CBS.STTM_ACCOUNT_CLASS~~
		- ~~account_class (code)~~
		- ~~description (product name)~~
-
	- dimension.cbs_acc_class (use this instead of ~~CBS.STTM_ACCOUNT_CLASS~~)
		- lookup.cbs_acc_class (unknow source) +
		- cbs.sttm_account_class  +
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