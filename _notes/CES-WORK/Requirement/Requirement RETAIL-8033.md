---

fc-calendar: My Calendar
fc-date: 
  year: 2022 
  month: November 
  day: 3
fc-category: Work 

---

Link: https://ces-ltd.atlassian.net/browse/RETAIL-8033

```ad-info
title: User Story
- As a billing user, I should be able to specify a start, end date, and trading partner (if applicable) for each billing address' assigned bill delivery method via Billing> Dual Billing> Summary Billing> Billing Address popup
- As a billing user, I should be able to specify a start, end date, and trading partner (if applicable) for each billing address' assigned bill delivery method via Customer Care> Billing Accounts Billing Address popup
```

```ad-info
title: Business Overview
Bill delivery methods can be set for each US state a client is active in; this allows flexibility for regulatory changes or client preferences/ business processes. After specifying bill presentation formats by state, clients can customize each individual billing account. To produce statements properly, a billing account must be configured for at least one of its state’s bill delivery methods. Then, each billing address under that billing account must be assigned at least one of the eligible bill delivery methods for its billing account.

Currently, a billing account address can be assigned more than one delivery option at a time; this results in 2 sections on the XML for bill delivery information. But there is no way to indicate the desire to switch from one method to another. For example, let's say a billing account on the paper bill option from 1/1/2020 - 4/1/2020 and then they'd like to switch to receiving EDI bills on 4/2/2020. Today, the process must be manually managed by a user and coordinated with the statement creation process. Since the address bill delivery method is not timebound, we have no way of differentiating that paper should end and EDI bill delivery option should begin. The code would read this as having both bill delivery options at the same time (which in cases is still valid).
```

```ad-note
title: Business Requirement
1. Add TradingPartnerID to blu.tbl_billing_account_bill_delivery_address_xref
    1. Backfill all trading partners for EDI bill based on their existing records in blu.tbl_billing_account_bill_delivery   
2. Add StartDate and EndDate to blu.tbl_billing_account_bill_delivery_address_xref   
    1.  Backfill all start dates as 1/1/2000 (so that the start dates are not NULL)    
3.  On the Delivery Methods popup, users should no longer see Trading Partner column
4.  On the Billing Address popup, a new accordion for each billing address should show an "Add new record" button and a sub-grid
    1.  sub-grid should contain the following columns: (below)
    2. “Assigned Bill Delivery Option” dropdown should be populated with the active Eligible Delivery Options for the billing account (existing functionality)
        i. Display blu.tbl_bill_delivery.DeliveryMethod in dropdown for every record in blu.tbl_billing_account_bill_delivery for the billing account where Active = 1
    3. “Trading Partner” dropdown should be populated with the active externally facing trading partners for the client (existing functionality)
        1. blu.tbl_trading_partner.External_TP = 1
        2. blu.tbl_trading_partner.Active = 1
        3. blu.tbl_trading_partner.ClientIntID maps to user logged in
        4. Display blu.tbl_trading_partner.TradingPartnerName in dropdown when “Assigned Bill Delivery Option” is EDI
        5. Trading Partner dropdown should be hidden when “Assigned Bill Delivery Option” is not EDI and NULL should be saved in the DB
    4. Validate that StartDate is before or equal to EndDate. If the user enters an invalid value, the system should not save the data and present an error message
    5. A billing account can have more than one assigned address bill delivery method for the same period as long as they are different option methods. Overlapping bill delivery method dates should be accepted as long as the BillDeliveryID is different. If the user enters an invalid value, the system should not save the data and present an error message
        1. for example, a billing account should be able to be on paper and EDI billing from 1/1/2020 - 4/1/2020. But the billing account should not be able to be on EDI billing for TradingPartner1 and TradingPartner2 at the same time
        2. for example, a billing account should be able to be on paper and EDI billing from 1/1/2020 - 4/1/2020. But the billing account should not be able to be on paper from 1/1/2020 - 4/1/2020 and paper again from 3/1-5/1
    6. A billing account cannot have exact duplicate assigned address bill delivery options. An exact duplicate would occur if all UI columns were identical as an existing row for the billing account. If the user enters an invalid value, the system should not save the data and present an error message

```

| UI Column Name           | UI Data Type | Data Source (where to save data into)                               | Optional vs Required                                                               |
|--------------------------|--------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Assigned Delivery Option | Dropdown     | blu.tbl_billing_account_bill_delivery_address_xref.BillDeliveryID   | Required                                                                           |
| Trading Partner          | Dropdown     | blu.tbl_billing_account_bill_delivery_address_xref.TradingPartnerID | Conditional (required when Assigned Delivery Option is “EDI” (BillDeliveryID = 3)) |
| Start Date               | Date picker  | blu.tbl_billing_account_bill_delivery_address_xref.StartDate        | Required                                                                           |
| End Date                 | Date picker  | blu.tbl_billing_account_bill_delivery_address_xref.EndDate          | Optional                                                                           |
| Active                   | Checkbox     | blu.tbl_billing_account_bill_delivery_address_xref.Active           | Required                                                                           |




Process
![[Retail-8033]]