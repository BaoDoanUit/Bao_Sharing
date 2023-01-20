### **User Story**
- Currently permission settings do not allow for restricting access to just the statement/invoice tab. The client is looking for further permission that will allow them to restrict access to that tab, but still give users access to remaining billing functionality.
- As a CES BLUE client, users should have access to functionality with the <mark class="hltr-pink">Dual Billing section</mark> but also be able to assign certain users which should have access to the Statement/Invoice screen while restricting others from having access.

### **Business Requirements**
#### Add option to CES BLUE > Billing > Billing Admin for Admin to configure permissions for users to have access to the “Statement/Invoice” screen from the Billing Dual list.
 - <mark style="color: #FF5582A6; background: transparent">Expectation is that only the “Access” checkbox</mark> would be available for the <mark class="hltr-red">“Statement/Invoice” option</mark> as currently there is no permission available to edit different parts of the “Statement/Invoice” screen. If desire is to have both read-only and read-update access, that may need to be addressed as a separate ticket.
   ![[Pasted image 20230109150502.png]]
- Users should be able to place a “check” on the “Statement/Invoice” box and save options.
#### Modify the CES BLUE > Billing > Dual Billing screen so that ONLY users who have permissions to the “Statement/Invoice” screen are able to see the corresponding tab.
- Logic within the “Statement/Invoice” screen should remain the same
- Users who do not have Statement/Invoice option checked under the Billing Admin screen but have other options enabled should be able to see the other tabs under the Dual Billing section but NOT the “Statement/Invoice” screen.