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
- kbz_iss_card_vw is final master table but some data are missing in kbz_iss_card_vw but data is in kbz_os_vw
- so need to join the two tables
-
- ```sql
  
  select
       case when c.card_type = 'MPU' then 'MPU'
            when c.card_type = 'UPI' then 'UPI'end as product
      ,a.cardholder_last_identity as nrc
      ,(b.aging_period  * 30) as dpd
   from cbs.kbz_iss_card_vw a
      join cbs.kbz_os_vw b  on a.card_number=b.card_number --- why need to inner join .
      join (select * from {{ ref('stg_lookup_card_product') }} where credit_contract='1' and card_type in ('UPI','MPU'))c on substring(a.card_number,1,8)=c.bin
      where  a.expiry_date >'31-DEC-23'
  
  ```
-
-
- ```sql
  
  select distinct source_code from cbs.cntb_asset_extract_details
  
  ODDATA	
  CARDDATA	--- ***
  HPDATA	 
  LOANDATA	
  FLEXCUBE	
  
  select
       case when a.productname like 'MPU%' then 'MPU'else 'UPI'end as product
      ,REGEXP_REPLACE(ID_NO, '\\s*\\([^()]*\\)$', '') as nrc
      ,case when a.acct = b.asset_reference_no then b.asset_earliest_ovd else 0 end as dpd
  from
      (select *from  {{ ref('stg_cbs_crd_lst') }} cl  
      where expir_date <='31-DEC-23'
       )a
  left join 
      (select * from {{ ref('stg_cbs_cntb_asset_extract_details') }} -- all loan with dpd filter with product_code
       where source_code='CARDDATA')b 
       on  a.acct = b.asset_reference_no
  ```
- stg_cbs_cntb_asset_extract_details = all loan with dpd group by with