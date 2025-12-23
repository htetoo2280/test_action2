- For loan dimension.cbs_loan_user is the main table.
  title:: loan_dpd
- daily loan dpd will support for dpd
-
- ## dpd days taking
	- ```sql
	  -- dpd updated only
	  select loan_acc
	        ,dpd_8am dpd
	  into #cte_loan_dpd
	  from derive.cbs_daily_loan_dpd
	  where loan_date::date = trunc(f_get_yesterday_mmt())
	  and   dpd_8am <> 0
	  and   source_code in ('LOANDATA','HPDATA','ODDATA')
	  ```
-
- ## loan outstanding from actb_history
	- ```sql
	  
	  -- opening only
	  select trn_date
	        ,loan_acc_no
	        ,os_amount prev_os_amount
	        ,tod_amount prev_tod_amount
	  into #cte_loan_opening_bal
	  from report.loan_daily_position
	  where trn_date::date = trunc(f_get_yesterday_mmt()) - 1   
	  -- os_amount is closing? , tod amount?? /// day - 2 closing mean day -1 opening
	  ```
-
-
- ```sql
  select asset_earliest_ovd,* from cbs.cntb_asset_extract_history where 
  asset_reference_no = '1962SL1222870001' order by extraction_dt_stamp
  
  select top 10 * from cbs.cltb_account_master where account_number = '1962SL1222870001'
  
  select top 10 * from cbs.actb_history where related_account = '1962SL1222870001'
  ```