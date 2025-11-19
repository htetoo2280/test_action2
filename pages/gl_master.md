- this table contain all gl and desc
- ```sql
  select sacs.account_class,
            sacs.dr_gl,
            ggd.gl_desc as dr_gl_desc,
            sacs.cr_gl,
            ggc.gl_desc as cr_gl_desc
       from {{ ref('stg_sttm_account_class_status') }} sacs
            left join {{ ref('stg_cbs_gltm_glmaster') }} ggd on sacs.dr_gl = ggd.gl_code
            left join {{ ref('stg_cbs_gltm_glmaster') }} ggc on sacs.cr_gl = ggc.gl_code
      where                                                     
           decode (sacs.status, 'NORM', 1, 0) = 1
  ```