# Point of Sale Features

You can't call these complete specifications, but rather starting points. You'll probably want to ask some questions of your customer.

## Sell One Item

I need to be able to sell one item at a time to a single shopper. 85% of my sales are a single item, so if this feature works, I can open my shop.

I have a barcode scanner that scans items, which simulates typing the barcode using the keyboard, and then pressing ENTER. I also have a display where I can display information about the scanned product. It's enough for now to display the price of the scanned product. We can add details later.

## Sell multiple items

I need to be able to sell multiple items to a single shopper as a single transaction. I expect to simply scan each product, one by one, then press a button to get the total amount to charge the customer. If you come up with some crazy way to do this, run it by me first.


## Sales taxes

In Canada, we add sales taxes at the cash register. On the product, the price tag will say $10, then we add taxes:

* GST, Goods and Services Tax, is 5% on all products
* PST, Provincial Sales Tax, is 8% in Ontario, but only some products require PST

For example, a $10 item with GST and PST will cost $11.30 at the cash register; however, when a shopper sees the product price, it must still say $10, because they expect to see that price.

THEREFORE, when I scan the product, I want to see this: "CAD 10.00 GP" (or "CAD 10.00 G" if the product does not require PST). Then I need to press a new key on the register called "TOTAL", and I need to see "CAD 11.30".


## Receipt

In Canada, we have to have details about the company, each item, the taxes on that item, the total taxes collected, the subtotal, and the grand total. It should look like this:

<pre>
12345  12.90 GP
23456   7.15 G
34567  34.90 GP
Subtotal  54.95
GST   2.76
PST  3.82
Total  61.53
</pre>

Maybe line up the decimal points.

Eventually, we'll replace the barcode with the name of the product, but don't worry about that now.

## Sales report, CSV version

I need a report showing all the sales so far. It's enough to just show me all the sales in the system. We'll talk about filtering later. The report should look like this:

<pre>
SALES REPORT as at 2011-10-13 15:24
"Date", "Subtotal", "GST", "PST", "Total"
"2011-10-12 19:24", "54.95", "2.76", "3.82", "61.53"
"2011-10-12 20:18", "13.00", "0.65", "0.00", "13.65"
...
"Total", "1982.45", "99.19", "104.25", "2185.89"
</pre>

I can be happy with comma-separated values for now (or semicolon-separated if you're in Europe). I can import this into a spreadsheet to analyse the results further.

**Valid CSV format, please.** This means quotation marks around fields, just to avoid any silliness when I import into a spreadsheet.

## Manual Override of Price

Sometimes scanning a product fails. Sometimes it succeeds and the price in the computer system doesn't match the price that the shopper expects to pay. (The price could be incorrect, out of date, missing…) In this case, the cashier needs to be able to enter the price directly. The cashier will have to decide whether the manually-entered price replaces the most-recently-scanned product (correcting an incorrect product) or not (compensating for a failed scan).

## Cash/Card report

I need a report showing all the sales paid by cash and all the sales paid by cards (credit card and debit card can go together). I want to be able to ask for each of these reports separately, or both of them together. The reports should look like the Sales Reports.


## Low inventory

When I sell a product, I want to be warned when I have 5 or fewer units of them left in stock.


## Check inventory

I want to be able to scan a product and see how many units of them I have in stock.


## Re-ordering report

I need a report showing all the products that I need to re-order. To start, I need to re-order any products whose inventory is low.


## Discounts

I want to be able to apply discounts. I can think of a few kinds of discounts to implement:

* percentage off the item
* amount off the item
* buy one, get one free
* percentage off the order
* amount off the order
* minimum quantity to purchase for an item discount
* minimum amount to spend for an order discount

Work with me to figure out which ones to do first. Remember that discounts come off the pre-sales-tax price.

## Pause/Resume Checkout

Cashiers sometimes need to pause and resume checking out a shopper. For example, a shopper wants to buy a product, but the scanned price is not correct, and so the cashier needs a manager's help to settle the dispute. This should not stop other shoppers from checking out. The cashier should be able to pause one shopper's transaction, allowing another shopper to finish, and then resume the previous shopper's transaction.

## New Sales Tax Rules

Our shop is moving to a new province with different sales tax rules. It is still true that some products have only GST (5%) and some products have both GST and PST, however:

- PST is now at the rate of 10%, and
- the calculation of PST is different: we add PST on top of GST.
- For example: a $100 product really costs ($100 + 5%) + 10% = $115.50. The GST portion of $5 and the PST portion is $10.50. (Be careful: there is a bug waiting to kill you here.)

## New New Sales Tax Rules
Our shop is not moving to a new province, but our province is adopting new sales tax rules. Now we have a single tax called HST (harmonized sales tax).

- HST is now at the rate of either 5% or 14%, depending on the product.
  - There is no easy rule for migrating existing products. Some products that had PST under the old rules have only 5% HST under the new rules.
- The new sales tax rules take effect in 23 days from whenever you read this. Of course, we have to handle returns/refunds accurately.

## Different Prices At Different Times

A product (barcode) might have different prices at different times, depending on some very arbitrary rules. I want to be able to define a rule that this "this is the price of that barcode during this period". Periods can overlap and conflict, so we need some mechanism to deal with this situation.

