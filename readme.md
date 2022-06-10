# Notes on Stellar operations

## Fee Bump

If you sent someone 100 xlm, they'd receive 100 minus the transaction fee. 
There might be a circumstance where you'd want to send 100 and them receive 100. 
The way to do this is with a fee bump which means bump the fee on to someone else, aka another account. 

You need the keys for the bump account

In the stellar lab create a normal transaction between sender and recipient, 
after signing the transaction there's a "wrap with fee bump" option. 

This takes the xdr of the payment operation and gives it to the fee bump operation. 
Add the bump public key, go to the sign page and replace the secret key that shows with the secret key from the bump account

## Bump Sequence

This is when you want to jump a transaction ahead in your own sequence timeline. 
Bum sequence is when you want 1 operation to invalid a bunch of other possible operations. 

For this there is a bump sequence operation

create a normal  operation
then add a bump sequence operation
the number has to be greater than your transaction sequence number
the source account is your own account
on the next page sign with your private key


## Adding a passphrase as an alternative signer. 

Set up an add options operation for the account
convert the passphrase to sha256 using any online converter
set the weight to 1 - this means this signer has the same importance as the account secret key and either can be used. 
Sign the transaction with the account private key
  
When you want to use the passphrase to sign a transaction 
You have to convert it to hexadecimal to be accepted by the signing field.  Use any online text to  hex converter. 
  
  
## Pre-authorized transactions

The purpose of a pre-authorised transaction is to create a transaction that is activated by the recipient, 
thus "pre authorized"
  
Create a transaction with a sequence number + 1, 
You don't have to sign or submit this transaction, copy the hash and the xdr
    
Create another transaction with the default sequence number (it will be ordered before the above one) 
operation set options
signer type = pre authorized transaction
past the hash 
set the weight to 1
      
sign and submit as usual 
    
the recipient can activate the transaction having been given the XDR
paste it into the endpoints, transactions, post transaction. 
    
  

## Sponsoring future reserves (create account)

  This allows an account to pay the base reserve(funding) for another account
  so you can create an account with balance 0, 
  
  To do this with create account:
  
A normal transaction with source account
      
1. Begin sponsoring future reserves
sponsored ID is the account you're going to create
2. Create account
destination is the account you're going to create
3. end sponsoring future reserves
source account is the account you've just created
          
Then sign the transaction with the private key of both accounts. 
      
 

## Sponsoring future reserves (create account)

  This allows an account to pay the base reserve(funding) for another account
  so you can create an account with balance 0, 
  
  To do this with create account:
  
A normal transaction with source account
      
1. Begin sponsoring future reserves
sponsored ID is the account you're going to create
2. Create account
destination is the account you're going to create
3. end sponsoring future reserves
source account is the account you've just created
          
Then sign the transaction with the private key of both accounts. 
      
## Create and claim claimable balance

1. generate 2 funded keypairs designated sender and receiver
2. build transaction
	source account = sender public key
	fetch next sequence number
	operation type = create claimable balance
	asset = native
	amount = whatevet 101
	claimants
		destination = receiver public key
		predicate = conditional 
		predicate type = not
		not predicate = conditional
		predicate type = time 
		time type = relative
		time value = 300
		(i.e. not before 300 seconds) 
	at the bottom sign in transaction signer
3. add senders secret key
	at bottom submit in transaction submitter
4. submit transaction
	"transaction succeeded with 1 operations

wait 5 mins

5. explore endpoints
	select resource = claimable balance
	all claimable balances
	sponsor = sender public key 
	submit
	find and copy id e.g. 000000002e5bdf568c53a17f54b4957bf571c4aa6f5f7ec4471403de3754257270a60744

6. build a transaction
	source account = receiver public key 
	fetch next sequence number
	operation type = claim claimable balance
	claimable balance id = paste id from #5
	at bottom sign in transaction signer
7. add receivers secret key
	at bottom submit in transaction submitter
8. submit transaction
	"transaction succeeded with 1 operations

9. explore endpoints
	accounts
	single account
	account id = receiver public key
	check balance - amount minus transaction fee
		
	
