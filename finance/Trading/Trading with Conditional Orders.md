### Trading with Conditional orders


https://scs.fidelity.com/webxpress/help/topics/learn_trading_conditional.shtml

Trading with Conditional Orders
A conditional order is an order executed based on an external trigger, such as a market condition, or the execution of another order linked to it. You can trade five types of conditional orders on Fidelity.com: Contingent, Multi-Contingent, One-Cancels-the-Other (OCO), One-Triggers-the-Other (OTO), and One-Triggers-a-One-Cancels-the-Other (OTOCO).

Fidelity offers conditional orders on a best efforts, "not held" basis. Use of Conditional Orders indicates your understanding and acceptance of the risks associated with these orders, so make sure you're familiar with and understand the trading risks associated with Conditional Orders before trading. Also, certain actions (i.e. short sells) and conditions (i.e. Immediate or Cancel (IOC) and Fill or Kill (FOK)) may not be available on a conditional order.

Contingent Orders
What is a Contingent order?
What are common uses for Contingent orders?
How do I establish a Contingent order?
When is my Contingent trade triggered?
What happens when my Contingent trade is triggered?
How often are index values updated?
What time constraints can I place on my Contingent order?
How do I cancel a Contingent order?
How do I change the expiration date, time or alert on my Contingent order?
How can I remove just the Contingent Criteria from a Contingent order?
Multi-Contingent Orders
What is a Multi-contingent order?
What are common uses for Multi-contingent orders?
How do I establish a Multi-contingent order?
How do the secondary criteria work (And at the same time, Or, Then)?
When is my Multi-contingent trade triggered?
What happens when my Multi-contingent trade is triggered?
How often are index values updated?
What time constraints can I place on my Multi-contingent order?
How do I change the expiration date, time or alert on my Multi-contingent order?
How do I cancel a Multi-contingent order?
How can I remove just the Contingent Criteria from a Multi-contingent order?
One-Cancels-the-Other (OCO) Orders
What is a One-Cancels-the-Other (OCO) order?
What is a common use of a One-Cancels-the-Other order?
When is buying power calculated for a One-Cancels-the-Other order?
Is there a reasonability check for One-Cancels-the-Other orders?
Where can I monitor my One-Cancels-the-Other order once I've entered it?
How do I change the expiration date, time or alert on my One-Cancels-the-Other order?
One-Triggers-the-Other (OTO) Orders
What is a One-Triggers-the-Other (OTO) order?
When is buying power calculated for a One-Triggers-the-Other order?
If my attempt to cancel my primary order is successful, what happens to my secondary order?
Are there any circumstances under which my secondary order might not be eligible for execution?
In a One-Triggers-the-Other order, can my primary and secondary orders have different times in force?
Where can I monitor my One-Triggers-the-Other order once I've made it?
How do I change the expiration date, time or alert on my One-Triggers-the-Other order?
One-Triggers-a-One-Cancels-the-Other (OTOCO) Orders
What is a One-Triggers-a-One-Cancels-the-Other order?
What is a common use of a One-Triggers-a-One-Cancels-the-Other order?
Where can I monitor my One-Triggers-a-One-Cancels-the-Other order?
How do I change the expiration date, time or alert on my One Triggers a Once Cancels the Other order?
How do I cancel a One-Triggers-a-One-Cancels-the-Other order?
Related Help Topics
Contingent Orders
What is a Contingent order?
Contingent Orders enable you to set a condition that will trigger the execution of an equity or single-leg option order. You can set a value for the following triggers for a stock, index or option contract:

Last Trade (eligible for stocks, indices and options)
Bid (eligible for stocks and options only)
Ask (eligible for stocks and options only)
Volume
Change % Up
Change % Down
52-week high
or 52-week low
Execution of an order is triggered if the equity, index or option contract is:

Greater than the trigger price
Greater than or equal to the trigger price
Less than the trigger price
Less than or equal to the trigger price
You can set "Time in Force" as either a Day Order or Good 'til Canceled. Once your condition is met, your order is placed as any of the following types:

Market
Limit
Stop Loss
Stop Limit
And all of the Trailing Stop Order types
Simply put, a Contingent Order gives you the choice to use several different conditions to trigger your Order.

Top
What are common uses for Contingent orders?
You can use a Contingent order to place an order once a stock has reached a new 52-week high or low. For example, a value investor may want to buy when a stock is at its low for the year. But a momentum trader might want to buy a stock when it has reached its high for the year. Either way a Contingent order can help.

You can also use a Contingent order to buy or sell an option based on the daily movement of the underlying stock by setting the criteria. For example, when IBM is up 5%, you want to sell a covered call against your 100 shares. A Contingent order enables you to set your option order to be sent to the market once IBM moved 5%.

You can also use a Contingent order to buy or sell a stock based on the daily movements of an index without monitoring the market tick by tick. So if the Dow Jones drops 3%, you may want to sell out of a certain position or buy a new stock.

Top
How do I establish a Contingent order?
Establish a Contingent order by identifying a specific trigger value for a stock, index or option contract. To use an index for a trigger price, select one of the several available from the drop-down list—a description of the index you select and a quote will appear on the right side of the conditional trade ticket.

Top
When is my Contingent trade triggered?
Your Contingent trade is triggered when the stock price, index value or option contract price is greater than, greater than or equal to, less than or less than or equal to the value you establish.

Top
What happens when my Contingent trade is triggered?
When your Contingent trade is triggered, it is sent to the marketplace for execution. Once triggered, a Contingent order appears on Order Details page as an open (triggered) order. To view the Contingent Criteria on Order Details for a Contingent order, select Details.

Certain Contingent orders may not be eligible for execution after being triggered for release to the marketplace, including limit or stop prices too far from the market or on the wrong side of the market. Please monitor these orders for reasonability. As a general guideline, an order may be cancelled if it is more than 30% away from the market, depending upon where it has been routed to for execution. You may receive a warning message when attempting to place a trade that fails a price reasonability check.

Top
How often are index values updated?
Consistent with industry standards, index values update at 15 second intervals. This may delay the release of your order to the marketplace.

Top
What time constraints can I place on my Contingent order?
A separate Time in Force (TIF) of Day or Good 'til Canceled (GTC) is allowed for the Contingent TIF and order TIF.

Behavior of Contingent orders with different TIF:

Contingent Criteria TIF	Order TIF	Behavior
Day	Day	Entire order is open for one day only.
Day	GTC	Trigger is open for 1 day only. If the criterion is triggered during this day, the order will be open for the 120 day GTC period* or until filled or canceled.
GTC	Day	Trigger will remain open for up to 120 days* or until triggered or canceled. Order will be open for the remainder of the day on which the criterion is triggered.
GTC	GTC	The entire Contingent order is open for 120 days maximum or until canceled or triggered. The order will remain open for the remainder of the 120 day GTC period*. For example, if the criterion is triggered on day 20, the order will be open for 100 days.

* The default GTC period for orders entered on Fidelity.com only is 180 days.
Top
How do I cancel a Contingent order?
You can attempt to cancel a Contingent order from the Order Details screen as you would any other type of order.

Top
How do I change the expiration date, time or alert on my Contingent order?
There are two ways to change the expiration date, time or alert on your Contingent order. On the Order Details page, click the 'Edit Expiration' link to update the date, time or alert on your order – then save your changes. You can also update these fields by canceling and replacing your order. On the Order Details page, click on the 'Attempt to Cancel & Replace' link and submit a cancel and replace order. Note – when using either the 'Edit Expiration' link or 'Attempt to Cancel & Replace' link on the Order Details page, each leg of your order will need to be updated individually.

Top
How can I remove just the Criteria from a Contingent order?
To remove the criteria from a Contingent order, go to the Orders page and select Attempt to Cancel and Replace, then select Remove Condition. Please note that removing the criteria from a Contingent order will make that order live in the marketplace.

Top
Multi-Contingent Orders
What is a Multi-Contingent order?
A Multi-Contingent order is an order that executes when two specified criteria are met, such as the achievement of a stock price and a particular index level. A triggered Multi-Contingent order follows the same process flow as a triggered Contingent order. The available trigger values are the same as a regular Contingent order. See available trigger values under â€˜What is a Contingent order?â€™.

Top
What are common uses of Multi-Contingent orders?
Multi-Contingent orders are used similarly to Contingent orders, but the orders are placed based on two criteria being met.: You choose whether you want the order placed if one or the other of the criteria is met, if both criteria are met at the same time, or if the criteria are met in sequential order. The dropdown selections for these conditions are Or, And at the same time, and Then

Examples of each type are below:

And at the same time: If stock XYZ has a 1.5% Change Up And at the same time has daily trade volume of 3 million shares then buy 500 shares XYZ at the market.
Or: If .DJI (Dow Jones Industrial Average) Last Trade is greater than 14,050 Or .IXIC (Nasdaq) Last Trade is greater than 2,850 then sell 250 shares ABC at a limit of $32.75.
Then: If stock ABC reaches a new 52-week high Then has a Last Trade greater than $37 then buy 250 shares ABC at trailing stop of 1%.
Top
How do I establish a Multi-Contingent order?
To establish a Multi-Contingent order, first specify the first set of criteria, which includes the trigger value for a stock index or option contract. To use an index for a trigger price, select one of the 30+ available from the dropdown menu. A description of the index you select and a quote will appear on the right side of the ticket.

Next, select how you want the second set of criteria to work with the first. Choose from And at the same time, Or, or Then, which also include a trigger value for a stock, index or option contract. Then set the trigger value for a stock, index or option contract.

Finally, specify the order you want to place if your criteria are met. Preview your order.

Top
How do the secondary criteria work (And at the same time, Or, Then)?
The order is placed when:

And at the same time – The first and second criteria are true at the same time
Or – Either the first or the second criteria is true
Then – The first criteria is met, and later the second criteria is met.
Top
When is my Multi-Contingent trade triggered?
Your Multi-Contingent trade is triggered when all of the specifications in each criterion are met according to the condition youâ€™ve selected: And at the same time, Or, Then.

Top
What happens when my Multi-Contingent trade is triggered?
When your Multi-Contingent trade is triggered, the order is sent to the marketplace for execution. Once triggered, a Multi-Contingent order appears on the Orders page as an open (triggered) order. To view the criteria, select Details. Note that there is no "partially triggered" state. All criteria must be met before the order is triggered.

Certain Multi-Contingent orders may not be eligible for execution after being triggered for release to the marketplace, including limit or stop prices too far from the market or on the wrong side of the market. Please monitor these orders for reasonability. As a general guideline, an order may be cancelled if it is more than 30% away from the market, depending upon where it has been routed to for execution. You may receive a warning message when attempting to place a trade that fails a price reasonability check.

Top
How often are index values updated?
Consistent with industry standards, index values update at 15 second intervals. This may delay the release of your order to the marketplace.

Top
What time constraints can I place on my Multi-Contingent order?
A separate Time in Force (TIF) of Day or Good 'til Canceled (GTC) is allowed for each criterion TIF as well as the order TIF.

Behavior of Multi-Contingent orders with different TIF:

Multi-Contingent TIF	Order TIF	Behavior
Day/Day	Day	
Entire order is open for one day only. If the order does not fill, it is canceled.

Or: On Day 1, one of the criteria is triggered. The order is released and is open for remainder of day.
Then: On Day 1, the first criterion is met, second criterion must be met same day. If second trigger is met, the order is released and is open for the remainder of the day.
And: Both criteria are true at the same time on Day 1. The order is released to the marketplace and is open for the remainder of the day.

Day/Day	GTC	


Criterion is open for one day only. If the criterion is triggered during this day, the order will be open for the 120 day GTC period* or until filled or canceled.

Or: On Day 1, one of the criteria is triggered. The order is released and is open for GTC.
Then: On Day 1, the first criterion is met, the second criterion must be met, same day. If second trigger is met, the order is released and is open GTC.
And: Both criteria are true at the same time on Day 1. The order is released to the marketplace and is open GTC.

* The default GTC period for orders entered on Fidelity.com only is 180 days.

GTC/GTC	Day	


Criterion will remain open for up to 120 days* or until triggered or canceled. Order will be open for the remainder of the day on which the criterion is triggered. If the order is released to the marketplace and does not fill, it is canceled.

Or: Within the GTC period, one of the criteria is triggered. The order is released and is open for remainder of day.
Then: Within the GTC period, the first criterion is met, second criterion must be met; within the remainder of the GTC period. If second criterion is met, the order is released and is open for the remainder of the day.
And: Within the GTC period, both criteria are true at the same time. The order is released to the marketplace and is open for the remainder of the day.

* The default GTC period for orders entered on Fidelity.com only is 180 days.

GTC/GTC	GTC	


The entire Multi-Contingent order is open for 120 days* maximum or until canceled or triggered. The order will remain open for the remainder of the GTC period. For example if the criterion is triggered on day 20, the order will be open for 100 days*.

Or: Within the GTC period, one of the criteria is triggered. The order is released and is open for remainder of GTC period.
Then: Within the GTC period, the first criterion is met, the second criterion must be met within the remainder of the GTC period. If second criterion is met, the order is released and is open for the remainder of the GTC period.
And: Within the GTC period, both criteria are true at the same time. The order is released to the marketplace and is open for the remainder of the GTC period.

* The default GTC period for orders entered on Fidelity.com only is 180 days.

Top
How do I change the expiration date, time or alert on my Multi-Contingent order?
There are two ways to do this. On the Orders page, select Edit Expiration to update the date, time, or alert on your order and then save your changes. You can also click Attempt to Cancel and Replace on the Orders page and use this process to modify the expiration date, time, or alert. Note: In either case, you will need to update each leg of your order individually.

Top
How do I cancel a Multi-Contingent order?
You can attempt to cancel a Multi-Contingent order from the Orders page as you would any other type of order. Cancellation requests are done on a "best efforts" basis.

Top
How can I remove just the criteria from a Multi-Contingent order?
To remove the criteria from a Multi-Contingent order, go to the Orders page and select Attempt to Cancel and Replace, then select Remove All Criteria.

Please note: You must remove both criteria, and doing so will make the order live in the marketplace.

Top
One-Cancels-the-Other Orders
What is a One-Cancels-the-Other (OCO) order?
A One-Cancels-the-Other order is an order whose execution results in the immediate cancellation of an order linked to it. Cancellation of the linked order happens on a "best efforts" basis.

In a One-Cancels-the-Other order, both orders may be live in the marketplace at the same time. The execution of either order triggers an attempt to cancel the unexecuted order. Partial executions will also trigger an attempt to cancel the other order.

Top
What is a common use of a One-Cancels-the-Other order?
One-Cancels-the-Other orders are commonly used to place orders on both sides of the market. For example, if an account is long in shares of XYZ stock, the account owner might enter a One-Cancels-the-Other order involving a sell limit for a certain number of XYZ shares above the market, and a stop loss for the same number of XYZ shares below this market. This takes advantage of an upward move in XYZ's price while protecting against a downward move.

Top
When is buying power calculated for a One-Cancels-the-Other order?
Buying power for a One-Cancels-the-Other order is calculated at the time of initial order entry, and is generally based on the more expensive of the two orders.
Top
Is there a reasonability check for One-Cancels-the-Other orders?
For retirement accounts only, there is a 2% percent minimum reasonability check for One-Cancels-the-Other orders on equities. For option OCO orders in retirement accounts, the premiums of the OCO must be at least $0.25 away from each other to prevent execution of both orders.

However, these reasonability checks are only intended to address the issue of reasonability—volatile market conditions may reduce their effectiveness. For example, if market conditions are volatile, it's possible for both orders in a One-Cancels-the-Other order to receive executions. It's also possible for one order to receive a delayed execution, resulting in the execution of both orders. You may receive a warning message when attempting to place an order that fails a price reasonability check.

Top
Where can I monitor my One-Cancels-the-Other order once I've entered it?
Monitor your One-Cancels-the-Other order on the Orders page. Each portion of your order has a unique identifier, but if you select Details for one, you'll see the details for the other as well.

Top
How do I change the expiration date, time or alert on my One-Cancels-the-Other order?
There are two ways to do this. On the Orders page, select Edit Expiration to update the date, time, or alert on your order and then save your changes. You can also click Attempt to Cancel and Replace on the Orders page and use this process to modify the expiration date, time, or alert. Note: In either case, you will need to update each leg of your order individually.

Top
One-Triggers-the-Other Orders
What is a One-Triggers-the-Other (OTO) order?
A One-Triggers-the-Other orders involves two orders—a primary order and a secondary order. The primary order may be a live order in the marketplace. The secondary order, held in a separate order file, is not. If the primary order executes in full, the secondary order is released to the marketplace and becomes live.

A OTO order can be made up of stock orders, single-leg option orders, or a combination of both.

Top
What is a common use of a One-Triggers-the-Other order?
One-Triggers-the-Other orders are commonly used to place a buy and sell order on the same security at the same time.

Top
When is buying power calculated for a One-Triggers-the-Other order?
Buying power for both the primary and secondary portions of a One-Triggers-the-Other order is calculated at the time of initial order entry, and may impact your ability to place other orders. A partial fill of your primary order will not release your secondary order to the marketplace. Additionally, a pending cancel primary order may, after some delay, be filled, resulting in the release of the secondary order to the marketplace.

Top
If my attempt to cancel my primary order is successful, what happens to my secondary order?
If your attempt to cancel your primary order is successful, your secondary order is canceled as well. It does not work the other way, however—a successful cancellation of a secondary order does not cancel a primary order.

Top
Are there any circumstances under which my secondary order might not be eligible for execution?
Even after being sent to the marketplace, a limit or stop secondary order may not be eligible for execution if it's far away from the market, or on the wrong side of the market. As a general guideline, depending on routing destination, an order more than 30% away from the market may be canceled. Please monitor your orders for reasonability. You may receive a warning message when attempting to place a trade that fails a price reasonability check.

Top
In a One-Triggers-the-Other order, can my primary and secondary orders have different times in force?
Yes, your primary and secondary orders can have different times in force.

Top
Where can I monitor my One-Triggers-the-Other order once I've entered it?
Monitor your One-Triggers-the-Other order on the Order Details page. The primary order and secondary order each have unique identifiers but if you select Details for one, you'll see the details for the other as well.

Top
How do I change the expiration date, time or alert on my One-Triggers-the-Other order?
There are two ways to do this. On the Orders page, select Edit Expiration to update the date, time, or alert on your order and then save your changes. You can also click Attempt to Cancel and Replace on the Orders page and use this process to modify the expiration date, time, or alert. Note: In either case, you will need to update each leg of your order individually.

Top
One-Triggers-a-One-Cancels-the-Other Orders
What is a One-Triggers-a One-Cancels-the-Other (OTOCO) order?
A One-Triggers-a One Cancels the-Other orders involves two orders-a primary order and two secondary orders. The primary order may be a live order in the marketplace while the secondary orders, held in a separate order file, are not. If the primary order executes in full, the secondary orders are released to the marketplace as a One-Cancels-the-Other order (OCO). The execution of either leg of the OCO order triggers an attempt to cancel the unexecuted order. Partial executions will also trigger an attempt to cancel the other order. An OTOCO order can be made up of stock orders, single-leg option orders, or a combination of both. It is possible during volatile market conditions that both legs of an OCO could receive executions. It is also possible that one order receives a delayed execution, resulting in the execution of both orders.

Top
What is a common use of a One-Triggers-a One-Cancels-the-Other order?
One-Triggers-a-One-Cancels-the-Other orders are commonly used to place a buy and corresponding sell orders (above and below the market) on the same security at the same time. The execution of the buy order triggers a One-Cancels-the-Other (OCO) order to sell. The execution of either leg of the OCO order triggers an attempt to cancel the unexecuted order.

Top
Where can I monitor my One-Triggers-a One-Cancels-the-Other order?
Monitor your One-Triggers-One-Cancels-the-Other order on the Orders page. The primary order and secondary orders each have unique identifiers, but if you select Details for one, you'll see the details for the other as well.

Top
How do I change the expiration date, time or alert on my One Triggers a One Cancels the Other order?
There are two ways to do this. On the Orders page, select Edit Expiration to update the date, time, or alert on your order and then save your changes. You can also click Attempt to Cancel and Replace on the Orders page and use this process to modify the expiration date, time, or alert. Note: In either case, you will need to update each leg of your order individually.

Top
How do I cancel a One-Triggers-a One-Cancels-the-Other order?
You can attempt to cancel a OTOCO order from the Orders page just as you would any other type of order. Cancellation requests are done on a "best efforts" basis.