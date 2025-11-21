## to finding all
- ```
  SELECT
      l.table_id,
      ti.schema || '.' || ti.table AS table_name,
      l.lock_owner AS xid,
      l.lock_owner_pid AS pid,
      l.lock_status,
      DATEADD(minute, 390, l.last_update) AS last_update_mmt,  -- +6h30m
      DATEADD(minute, 390, l.last_commit) AS last_commit_mmt,  -- +6h30m
      DATEDIFF(second, l.lock_owner_start_ts, GETDATE()) AS lock_duration_seconds
  FROM stv_locks l
  LEFT JOIN svv_table_info ti
         ON l.table_id = ti.table_id
  ORDER BY l.last_update DESC;
  
  ```
-
- ## finding with table_id
- ```
  
  SELECT 
      table_id,
      lock_owner_pid AS pid,
      lock_owner AS xid,
      lock_status,
      last_update
  FROM stv_locks
  WHERE table_id = 47793037;
  
  SELECT pid, user_name, status, starttime, duration, query
  FROM stv_recents
  WHERE pid IN (
      SELECT lock_owner_pid
      FROM stv_locks
      WHERE table_id = 47793037
  );
  
  ```
-
- ## unlock on pid
- ```
  SELECT pg_terminate_backend(23118);
  ```
-
- ## check running process
- ```
  select * from stv_recents  where status <> 'Done' order by starttime desc 
  ```
-
- --------------------
-
- ## update
- ```sql
  
  SELECT oid, relname ,*
  FROM pg_class
  WHERE relname = 'kpay_cust_profile';  ---50672073
  
  SELECT c.oid, n.nspname AS schema, c.relname AS table_name
  FROM pg_class c
  JOIN pg_namespace n ON n.oid = c.relnamespace
  WHERE n.nspname = 'dimension'
    AND c.relname = 'kpay_cust_profile';
  
  
  SELECT * 
  FROM stv_locks
  WHERE table_id = '50672073';
  
  SELECT *  ---- invisable lock
  FROM stv_recents
  ORDER BY starttime DESC;
  
  SELECT *
  FROM stv_inflight;
  
  SELECT *
  FROM SVV_TABLE_INFO
  WHERE table_id = '50672073';
  ```
-
- ပြန်စစ်