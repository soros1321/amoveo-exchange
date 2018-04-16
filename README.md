amoveo_exchange
=====

This is a work in progress. It does not yet function as an exchange.





This is an exchange written for trades between bitcoin and amoveo.

===  turn it on
```
sh start.sh
```

=== attach to exchange so you can issue commands
```
sh attach.sh
```
you can detach by holding the control key and pressing the D key.


The order book matches trades in single-price batches.
It selects a price to match as many trades as possible.
It prefers the price where people who are buying Veo are getting the best deal possible.


It is a shapeshift style exchange. There are no accounts or passwords.
You give the details of the trade you want to make, and we provide an address to send your coins to, and a Trade-ID so you can look up the status of your trade.
Each trade has a customizable time limit. If your trade doesn't get matched or only gets partially matched by the time limit, then we refund your remaining balance.

The trade's status goes through these stages:
1) unfunded
2) unconfirmed
3) unmatched
4) partially matched
5) matched


during steps 1 and 2 the trade is owned by the unconfirmed gen_server.

during steps 3 and 4 the trade is owned by the order_book gen_server.

During step 5 the trade is owned by the trade history gen_server.

Additionally, we have a gen_server for knowing which stage the trade is in so we know where to look it up.




====== Warnings

* If you ever deleted the database for any reason, it is important to change your public key in the full node. Otherwise you could accept payments from your history that are no longer valid. Allowing people to trade in your market without paying you.