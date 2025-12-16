## cbs.actb_history (transaction table)
	- if want to take gl , use cbs.actb_history
	- ```sql
	  select ac_branch,sum(case when drcr_ind = 'C' then lcy_amount else lcy_amount* -1 end) as lcy_bal from cbs.actb_history 
	  where  len(ac_no) = 17 group by ac_branch 
	  order by ac_branch
	  ```
-
-