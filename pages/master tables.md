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
-
- ------
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