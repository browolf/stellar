Notes on Stellar operations

Fee Bump

If you sent someone 100 xlm, they'd receive 100 minus the transaction fee. 
There might be a circumstance where you'd want to send 100 and them receive 100. 
The way to do this is with a fee bump which means bump the fee on to someone else, aka another account. 

You need the keys for the bump account

In the stellar lab create a normal transaction between sender and recipient, 
after signing the transaction there's a "wrap with fee bump" option. 

This takes the xdr of the payment operation and gives it to the fee bump operation. 
Add the bump public key, go to the sign page and replace the secret key that shows with the secret key from the bump account

Bump Sequence

This is when you want to jump a transaction ahead in your own sequence timeline to invalid 

Bum sequence is when you want 1 operation to invalid a bunch of other possible operations. 

For this there is a bump sequence operation

create a normal  operation
then add a bump sequence operation
  the number has to be greater than your transaction sequence number
  the source account is your own account
on the next page sign with your private key
