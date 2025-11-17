- **auditing and row count checking in oracle**
- ```oracle
  SELECT DISTINCT ORA_ROWSCN,SCN_TO_TIMESTAMP(ORA_ROWSCN) FROM SFCUBS.ICTB_UDEVALS 
  WHERE trunc(UDE_EFF_DT) = TO_DATE('20250505','yyyymmdd') 
  AND trunc(SCN_TO_TIMESTAMP(ORA_ROWSCN)) = TO_DATE('20250506','yyyymmdd')
  ORDER BY SCN_TO_TIMESTAMP(ORA_ROWSCN)
  ```
-
- **auditing rows in redshift**
- ```redshift
  SELECT 
      DATEADD(minute, 390, i.starttime) as last_insert_time,
      u.usename as user_name,
      t.schema as schema_name,
      t.table as table_name
  FROM stl_insert i
  JOIN pg_user u ON i.userid = u.usesysid
  JOIN svv_table_info t ON i.tbl = t.table_id
  WHERE t.schema = 'lookup'
    AND t.table = 'cbs_cust_segment'
  ORDER BY i.starttime DESC
  LIMIT 1;
  ```
-