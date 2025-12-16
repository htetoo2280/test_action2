## CBS.STTM_CUST_ACCOUNT
	- (cust_ac_no,cust_no)
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
-