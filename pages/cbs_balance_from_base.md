- getting daily balance from base model (basic)
- ```sql
  
  select
      -- c.TheDate,
      -- top 10
      b.branch_code,
      
      sum(b.lcy_bal) LcyClosingBal
  into #daily_base
  from Dimension.Calendar c
  inner join base.cbs_acc_bal_trn b
  on c.TheDate BETWEEN b.from_date and b.to_date
  inner join lookup.cbs_acc_class a 
  on substring(b.acc_no,4,3)=a.acc_class
  where c.TheDate >= '2025-02-01' and c.thedate <= '2025-02-28' and a.deposit_flag = 'Y'
  group by branch_code
  ```