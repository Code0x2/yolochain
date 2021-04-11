# YoloChain

Its HOT(holochain) but it baits bots instead. 

# How it works 
The token is a standard ERC20 token, modified to query a seperate, upgradable contract for true transfer amounts. Example

[Bob tries to transfer 100 YOT to Alice]

➥ [YOT] -> [FM3]

   ➥ [Transfer 100 YOT from Bob to Alice] returns (50)
               
➥ <End; Bob: 0, Alice: 50>

The external contract enforces the amount received by the receiving user, or can revert if the transaction shouldn't happen, but the full amount is removed from sender

# Baiting bots that use FlashBots
Most bots that use flashbots dont double check tokens if theyre sellable or not, because the bundle wont be included unless miner coinbase is paid (typically in the trailing sell tx). However reverting transactions are able to be included, if the rest of the bundle is profitable.
Knowing this, all we have to do is pay the miner instead of the frontrunning bot. However if we pay the miner regardless, the bundle will not be included because of profit switching (a non-flashbots block will be added if the flashbots block is less profitable). So we must make sure that we only pay the miner if it is apart of the bundle. 
This can be done via adding a tracker that will track if the token has been bought in that block. If it has, then allocate funds to coinbase, else just proceed as a normal tx.

### Wen protecc? idk. good luck?
