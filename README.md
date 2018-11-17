Problem statement: find out if a user into either eligible or not eligible for loan ,given the following data

[ Download Full dataset ](https://github.com/IBMDevConnect/RBSHack2018/raw/master/hackdata/hack_data_v1.zip)
# Understanding the dataset
the following list explains what each row stands for
* member_id is a personal identifier, do not want to include this in modeling.
* loan_amnt is the listed amount of the loan applied for by the borrower. If at some point in time, the credit department reduces the loan amount, then it will be reflected in this value.
* funded_amnt is the total amount committed to that loan at that point in time.
* funded_amnt_inv is not the same as funded_amt - total amount committed by investors for that loan at that point in time.
* term is the length of time the loan was given ['36 months', '60 months'].
* batch_enrolled classes a loan in one of 105 batches. Need to explore further.
* int_rate is the interest rate.
* grade is a categorical variable, A through G.
* sub_grade is another catagorical variable, as above but with groups 1-5 for each letter.
* emp_title is maybe job title? 190125 unique values in the training data.
* emp_length is number of years employed, categorical, < 1 year to 10 + years.
* home_ownership is status of housing, one from ['OWN', 'MORTGAGE', 'RENT', 'OTHER', 'NONE', 'ANY'].
* annual_inc is the amount the applicant earns. Continuous variable.
* verification_status is unclear what is being verified. Categorical, one of ['Source Verified', 'Not Verified', 'Verified'].
* pymnt_plan is y or n.
* desc is free-text description of why the loan has been applied for, e.g. "My goal is to obtain a loan to pay off my high credit cards and get out of debt within 3 years."
* purpose is a categorical variable with reason for taking the loan, one from ['debt_consolidation', 'home_improvement', 'credit_card', 'other','major_purchase', 'small_business', 'vacation', 'car', 'moving', 'medical', 'wedding', 'renewable_energy', 'house', 'educational']
* title is another category with info as to why the loan was taken out. 39694 unique values.
* zip_code is first 3 chars of zip code, 917 uniques
* addr_state are state codes
* dti is some value, borrower's debt to income ratio, calculated using the monthly payments on the total debt obligations, excluding mortgage, divided by self-reported monthly income
* delinq_2yrs is integers, 0 through 30 and NaNs. Number of late payments in last 2 years?
* inq_last_6mths is integers, 0 through 31 and NaNs. Number of late payments in last 6 months?
* mths_since_last_delinq is int of months since last late payment
* mths_since_last_record is another int, not sure what the record is..
* open_acc is another int. The number of open credit lines in the borrower's credit file.
* pub_rec is another int. Number of derogatory public records.
* revol_bal is another int. Total credit revolving balance.
* revol_util is a 1 decimal place float. Revolving line utilization rate, or the amount of credit the borrower is using relative to all available revolving credit.
* total_acc is another int. The total number of credit lines currently in the borrower's credit file.
* initial_list_status values are 'w' or 'f'. Unsure.
* total_rec_int are float values, interest recieved to date.
* total_rec_late_fee are float values, total recieved in late fees.
* recoveries could be amount recovered. Float values. Mainly 0.00.
* collection_recovery_fee could be fee charged for collecting the recovery. Mainly 0.00.
* collections_12_mths_ex_med - Number of collections in 12 months excluding medical.
* mths_since_last_major_derog is number on months since last most recent 90-day or worse rating
* application_type is whether the application is ['INDIVIDUAL', 'JOINT']
* verification_status_joint is [nan, 'Verified', 'Not Verified', 'Source Verified'] - verification status where application is joint. train_df[['verification_status_joint', 'application_type']].where(train_df['application_type'] == 'JOINT').dropna()
* last_week_pay is a category, 98 values.
* acc_now_delinq is the number of accounts on which the borrower is now delinquent. Int.
* tot_coll_amt is the total collection amounts ever owed.
* tot_cur_bal is the total current balance of all accounts. total_rev_hi_lim is the total revolving high credit/credit limit.
* loan_status is the current status of the loan.

# Actions performed

* Remove ['member_id', 'batch_enrolled', 'desc']
* Integer encode: ['emp_length', 'delinq_2yrs', 'inq_last_6mths', 'mths_since_last_delinq', 'mths_since_last_record', 'pub_rec', 'total_acc', 'open_acc', 'collections_12_mths_ex_med', 'acc_now_delinq', 'last_week_pay']
* One hot encode: ['term', 'grade', 'sub_grade', 'home_ownership', 'verification_status', 'pymnt_plan', 'purpose', 'addr_state', 'initial_list_status', 'application_type', 'verification_status_joint', ]
* Leave as-is: ['annual_inc', 'dti', 'revol_bal', 'revol_util', 'total_acc', 'total_rec_int', 'total_rec_late_fee', 'recoveries', 'collection_recovery_fee', 'tot_coll_amt', 'tot_cur_bal' 'total_rev_hi_lim', 'open_acc', 'mths_since_last_major_derog']
* Unsure: ['member_id', 'emp_title', 'title', 'zip_code']
