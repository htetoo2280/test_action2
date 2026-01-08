- **Revaluation (ဘဏ်လုပ်ငန်းအတွင်း Revaluation Transaction)** ကို လွယ်လွယ်ကူကူရှင်းပြရမယ်ဆိုရင်
- 👉 **နိုင်ငံခြားငွေ (Foreign Currency) နဲ့ဆိုင်တဲ့ လက်ကျန်တွေကို လက်ရှိ Exchange Rate နဲ့ ပြန်တွက်ခြင်း** ဖြစ်ပါတယ်။
-
- ## ဘာကြောင့် Revaluation လုပ်ရတာလဲ?
	- **Financial Statement မှာ တန်ဖိုးမှန်ဖို့**
	- **Exchange Gain / Loss ကို သိဖို့**
	- **Central Bank / Auditor requirement အရ**
	- **End of Day / End of Month Process အဖြစ်**
-
- ## Accounting Entry (Conceptually)
	- ### Gain ဖြစ်ရင်
		- Debit : FCY Asset Account
		- Credit : Revaluation Gain (P&L)
	- ### Loss ဖြစ်ရင်
		- Debit : Revaluation Loss (P&L)
		- Credit : FCY Asset Account
- (ဘဏ်စနစ်အလိုက် GL structure ကွာနိုင်ပါတယ်)
-
- ## Banking System အတွင်းမှာ Revaluation ကို ဘယ်အချိန်လုပ်လဲ?
	- **Daily EOD**
	- **Month End / Year End**
	- **Before Financial Reporting**
	- **CBM Reporting**
-
- ### Exchange Rate
  
  | Type | Rate |
  | ---- | ---- | ---- |
  | Previous Rate | 2,000 MMK |
  | Revaluation Rate (EOD) | 2,050 MMK |
  
  ---
- ## Step 1️⃣ CBS – Original Balance (Before Revaluation)
  | Field | Value |
  | ---- | ---- | ---- |
  | Account No | SA-USD-001 |
  | FCY Balance | 10,000 USD |
  | LCY Book Value | 20,000,000 MMK |
  | Rate Used | 2,000 |
  
  👉 ဒီအချိန်မှာ GL ထဲမှာ already booked ဖြစ်ပြီးသား
- ### GL Snapshot (Before)
  | GL Code | GL Name | Dr | Cr |
  | ---- | ---- | ---- |
  | 101010 | FCY Saving Control (USD) | 20,000,000 | – |
  
  ---
- ## Step 2️⃣ Revaluation Trigger (EOD Job)
  CBS Revaluation Engine က
  👉 **FCY Balance × New Rate** နဲ့ ပြန်တွက်
  
  ```
  10,000 × 2,050 = 20,500,000 MMK
  ```
- ### Difference
  
  ```
  20,500,000 – 20,000,000 = +500,000 MMK
  ```
  
  ➡️ **Unrealized Exchange Gain**
  ---
- ## Step 3️⃣ Revaluation Transaction (CBS Level)
  
  CBS ထဲမှာ **System Generated Transaction** တစ်ခု create လုပ်ပါတယ်
  
  | Field | Value |
  | ---- | ---- | ---- |
  | Tran Code | FX_REVAL |
  | Tran Date | 31-03-2026 |
  | FCY Amount | 0 |
  | LCY Amount | +500,000 |
  | Event | Revaluation |
  | Reversal Flag | N |
  
  ---
- ## Step 4️⃣ GL Posting (Accounting Entry)
- ### 📌 GL Entries – Revaluation Gain
  
  | GL Code | GL Name | Debit | Credit |
  | ---- | ---- | ---- |
  | 101010 | FCY Saving Control (USD) | 500,000 | – |
  | 701020 | FX Revaluation Gain (P&L) | – | 500,000 |
  
  👉 **Balance Sheet Account** တန်ဖိုးတက်
  👉 **P&L မှာ Gain ထွက်**
  ---
- ## Step 5️⃣ GL Balance After Revaluation
  
  | GL Code | GL Name | Balance (MMK) |
  | ---- | ---- | ---- |
  | 101010 | FCY Saving Control | 20,500,000 |
-
- summary
	- revaluation process ကိုနားလည်ဖို့ အတွက် snapshort ယူတာရယ် gain and lost ကို p&l ထဲ တန်းပေါင်းထည့် သင့် မထည့် သင့် နဲ့ gain and lost ကို reversal လုပ်မလုပ် ဆို တာတွေကို သိထားရမှာပါ
	- finance ရဲ့ accounting flow ချထားတဲ့ အပေါ်မူတည်ပြီး org တစ်ခုနဲ့ တစ်ခု မတူနိုင်ပါဘူး
-
- အသုံးများတဲ့ ပုံစံတစ်ခုကတော့ (for gain)
	- EOD step ထဲမှာ အရင်ဆုံး FCY Control account ထဲက ထုတ်ပြီး gain ထဲထည့်လိုက်ပါတယ်
	- အဲအချိန်မှာ snapshot ယူပြီး gain balance (on base rate) ကို store လုပ်ပါတယ်
	- ပြီးတာနဲ့ အဲ transaction ကို reversal လုပ်ပါတယ်
	- ပြီးရင် FCY Control account mmk ကို market rate နဲ့ပြန်သင့်ခဲ့တာက နောက်ဆုံး အဆင့်ပါ
	- မှတ်ချက် - တစ်ရက် ပြီးတစ်ရက် အကုန်လုံးကို ပြန်ပြန် revaluation လုပ်တာကြောင့်မို့ reconciliation မှာအထောက်ကူဖြစ်စေပါတယ်
-
- remark
	- base rate ဟာ မနေ့က rate နဲ့ မတူပါဘူး
	- base rate ကို GL ကို စတင်ဖွင့်ကတည်းက အမှန်တကယ်သင့်ခဲ့တဲ့ rate လို့သတ်မှတ်ပါတယ်
-
- အဲလိုဆို -
	- gain ကို profit ထဲထည့်ရမယ်ဆို အများကြီး gain သလိုဖြစ်နေနိုင်တယ်
	- အဲတာကို ရှောင်ဖို့နည်းလမ်း အချို့ ရှိနိုင်ပါတယ်
-
-