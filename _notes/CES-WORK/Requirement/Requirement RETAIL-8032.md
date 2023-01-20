Link: https://ces-ltd.atlassian.net/browse/RETAIL-8032

```CSharp
public class BillDeliveryAddressModel
{
    public int BillingAccountID { get; set; }
    public int BillDeliveryID { get; set; }
    public string DeliveryMethod { get; set; }
    public bool Active { get; set; }
    public bool MainAddress { get; set; }
    public int BillingAddressID { get; set; }
    public string BillingAccountName { get; set; }
    public string BillingAddress1 { get; set; }
    public string BillingAddress2 { get; set; }
    public string BillingCity { get; set; }
    public string BillingStateCode { get; set; }
    public int BillingStateID { get; set; }
    public string BillingZip { get; set; }
    public string BillingContactNumber { get; set; }
}
```

![[RETAIL-8032 | 1000x800]]
Alter table
