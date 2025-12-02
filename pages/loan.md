- For loan dimension.cbs_loan_user is the main table.
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