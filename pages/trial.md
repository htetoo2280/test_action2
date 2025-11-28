## Checking Table
	- ```sql
	  select ac_branch,ac_no,sum(case when drcr_ind = 'C' then 
	  lcy_amount else lcy_amount* -1 end) as lcy_bal from cbs.actb_history 
	  where  ac_no = '100300465' group by ac_branch,ac_no 	
	  
	  
	  select sum from derive.cbs_daily_gl_bal_trn where 
	  bkg_date = '2025-11-27' and gl_code = '100300465'
	  ```
-
-
- correct trial model is derive.cbs_daily_gl_bal_trn
- this is coming from staging.stg_acoe_cbs_staging_opening
-
- ![image.png](../assets/image_1763541551609_0.png)
-
- staging.stg_acoe_cbs_staging_opening (using cbs.actb_history)
	- this is the customer account level opening, transaction and closing.
	- because of the nature of OD and current account.
	- so need to define as credit_gl or debit_gl to get a correct trial.
-
- cbs_daily_gl_bal_trn
	- this is the final model of trial balance that is converted to correct gl.
-
-