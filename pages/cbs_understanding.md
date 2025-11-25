## base.cbs_acc_bal_trn
- ```sql
  select branch_code,sum(lcy_bal) as lcy_bal from base.cbs_acc_bal_trn 
  where is_current = 1 group by branch_code order by branch_code
  ```
-
	- cbs.actb_bal_history --- > base.cbs_acc_bal_trn
	- this is correct for len(ac_no) = 17  (only diff 3000 ks in 999 branch)
-
- ## cbs.actb_history (transaction table)
-
-
-
- tran
  accounting entries = trn table (cbs.actb_history)
  actb_daily_log (daily)
  unsuccess ?
  
  master
  actb_accbal_history (balance)
  ---------------------------
  as of aprial 2023
  
  adapter.srv_tb_ad_central_txn_log (function code to define product)
-
- ## detail
-
-
- ![image.png](../assets/image_1763522433952_0.png)
-
- ##
- product master
- to join for product category
- ![image.png](../assets/image_1763523198135_0.png)
-
-
- [[general_cbs_layer]]
- [[gl_master]]
- [[trial]]
- [[loan]]
-
-