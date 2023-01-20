Link: https://ces-ltd.atlassian.net/browse/RETOPS-25295

Issue: We see some statement has LateFee = 0; However, underlying lateFee <> 0. There are no human updates for the statement.

Code
``` SQL
select * from retail_Billing.bil.tbl_statement s 
left join retail.blu.tbl_billing_account_charge ba on ba.stmtID = s.StmtID where isnull(ba.iswaived,0) <> 1 
and s.LateFee <> ba.amount 
and s.LateFee = 0

select * from retail_Billing.bil.tbl_statement s 
where s.stmtID = 5740686  

select * from retail.blu.tbl_billing_account_charge ba 
where stmtID = 5740686
```

The current process sum LateFee = 0 in tbl_statement
