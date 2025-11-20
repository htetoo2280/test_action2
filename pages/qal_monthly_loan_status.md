-
- ```sql
  
  select org_reg_short_code as org_onboarded_short_code
        , id_type as id_type
        , unique_id as id_number
        , acc_status as status
        , reg_date_time as date_registered
        ,dateadd(day, -1, date_trunc('month', f_getdate_mmt())) as data_date
  from  base.kpay_org_details 
  where sub_org_type not in ('Employee Agent','Employee Agent Teller') -- <> employee
  and is_current = 1
  and acc_status <> 'Closed'
  ```
-
- do not take employee with sub_org_type not in ('Employee Agent','Employee Agent Teller') -- <> employee
-
- org_reg_short_code is main id in