-
- ## this is use for deleting branch skip master
-
- ```
  git branch --merged master | ForEach-Object {
      $branch = $_.Trim()
      if ($branch -ne 'master' -and $branch -ne '* master') {
          git branch -d $branch
      }
  }
  ```