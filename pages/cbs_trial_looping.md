- I have create to loop with 2 procedure
- the first one is normal query and insert to table
- the second one is loop the first query
-
- ## create table
- ```sql
  CREATE TABLE backups.summed_closing (
      trn_date DATE,
      opening DECIMAL(34,4),
      tran DECIMAL(34,4),
      closing DECIMAL(34,4)
  
  );
  ```
- ## the first stro
- ```sql
  
  CREATE OR REPLACE PROCEDURE integration.sp_insert_summed_closing()
  LANGUAGE plpgsql
  AS $$
  DECLARE
      v_last_date DATE;
      v_opening NUMERIC(18,2);
      v_tran NUMERIC(18,2);
      v_closing NUMERIC(18,2);
      v_start_date DATE;
      v_end_date DATE;
  BEGIN
      
      SELECT COALESCE(trn_date, '2018-06-30'), COALESCE(closing, 0)
      INTO v_last_date, v_opening
      FROM backups.summed_closing where trn_date = (select max(trn_date) from backups.summed_closing); 
  
      v_start_date := date_trunc('month', v_last_date) + interval '1 month';
      v_end_date := (date_trunc('month', v_last_date) + interval '2 month') - interval '1 day';
  
  
      SELECT SUM(CASE WHEN drcr_ind='D' THEN lcy_amount * -1 ELSE lcy_amount END)
      INTO v_tran
      FROM cbs.actb_history
      WHERE ac_no IN ('280103101','190133001','285101138','131401001','231401001')
        AND trn_dt BETWEEN v_start_date AND v_end_date;
  
      -- Calculate closing
      v_closing := v_opening + COALESCE(v_tran, 0);
  
      -- Insert new month record
      INSERT INTO backups.summed_closing(trn_date, opening, tran, closing)
      VALUES (v_end_date, v_opening, COALESCE(v_tran, 0), v_closing);
  
  END;
  $$;
  ```
-
- ## the second stro
- ```sql
  
  CREATE OR REPLACE PROCEDURE integration.insert_loop()
  LANGUAGE plpgsql
  AS $$
  DECLARE
      i INT := 0;
  BEGIN
      WHILE i < 8 LOOP
          -- Call your existing procedure
          CALL integration.sp_insert_summed_closing();
  
          -- Increment the counter
          i := i + 1;
      END LOOP;
  END;
  $$;
  ```