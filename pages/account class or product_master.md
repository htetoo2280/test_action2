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
	-