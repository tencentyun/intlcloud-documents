## Pay-on-Behalf Access Requirements

Requirements for enabling pay-on-behalf mode: When a member account joins an organization, the account must meet the following requirements to enable the pay-on-behalf mode:

<table>
  <tr>
  <th><b>Object</b></th>
  <th><b>Condition</b></th>
    </tr>
   <tr>
      <td rowspan=3>Member account</td>
    <td>Account verification: <br/>1. Member and admin accounts must be <b>verified with the same enterprise identity</b> at Tencent Cloud. <br/>2. Agents and their customers cannot select the financial pay-on-behalf mode. <br/>3. Resellers and their customers cannot select the financial pay-on-behalf mode.</td>
   </tr>
   <tr>  
	<td>Account type verification: <br/>1. External accounts or internal accounts of type 4, 6, or 9: The available balance in the member account should be greater than or equal to 0. <br/>2. Internal accounts of other types: Not verified.</td>
	</tr>
	<tr>  
	<td>Order verification: <br/>The member account cannot have orders to be paid, renewed, or refunded. <br/>Order status: To be paid or processing.</td>
	</tr>
	<tr>
	<td>Admin account</td>
	<td>Currently, only the admin account can be the payer account, while agents, resellers, and their customers cannot. <br/>1. External accounts or internal accounts of type 4, 6, or 9: The payer account <b>has no overdue payments or has an available balance greater than or equal to 0. </b>.<br/><b>2. Internal accounts of other types: Not verified</b>.</td>
	</tr>
	<tr>
</table>



Requirements for disabling pay-on-behalf mode: When a member account quits an organization, the account must meet the following requirements to disable the pay-on-behalf mode:

<table>
  <tr>
  <th><b>Object</b></th>
  <th><b>Condition</b></th>
    </tr>
   <tr>
      <td rowspan=3>Member account</td>
    <td>Account type verification: <br/>1. External accounts or internal accounts of type 4, 6, or 9: The available balance in the member account should be greater than or equal to 0. <br/>2. Internal accounts of other types: Not verified.</td>
   </tr>
   <tr>  
	<td>Order verification: <br/>The member account cannot have orders to be paid, renewed, or refunded. <br/>Order status: To be paid or processing.</td>
	</tr>
	<tr>  
	<td>Card verification: <br/>Mid- and long-tail member accounts not followed up by channel managers should have a bound credit card.</td>
	</tr>
</table>

