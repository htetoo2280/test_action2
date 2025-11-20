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
- org_reg_short_code is main id in base.kpay_org_details
-
- ```sql
  select  
  'VISA' product
  ,customer_last_identity as nrc
  ,(aging_period  * 30) AS dpd 
  from  {{ ref('stg_cbs_kbz_os_vw') }}  
  where substring(card_number ,1,6)='421686')
  
  select * from lookup.card_product
  
  what credit_contract mean? 
  bin	credit_contract	card_type
  40671600	0	VISA	
  42168600	1	VISA	
  42168620	1	VISA	
  42168621	1	VISA	
  42168670	1	VISA	
  42168671	1	VISA	
  45376500	0	VISA	
  kbz_os_vw --  
  kbz_iss_card_vw -- master
  ```
-
- kbz_iss_card_vw is final master table but