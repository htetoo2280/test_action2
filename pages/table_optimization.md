- data are store in slices and parallel scan.
-
- Cluster
   ├─ Node1
   │   ├─ Slice1
   │   └─ Slice2
   └─ Node2
       ├─ Slice1
       └─ Slice2
-
- ## diststyles
- ![image.png](../assets/image_1763612605367_0.png)
-
- **Observation:**
- Slice တစ်ခုချင်း scan → parallel scan → query fast
- Note column သာပေါင်းပြီး scan → slice အလိုက် storage
-
- ------------
-