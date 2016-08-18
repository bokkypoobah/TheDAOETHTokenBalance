# TheDAOETHTokenBalance

Scripts and data to compute the balances of The DAO token holders on the hard-forked Ethereum chain.

<br />

---

# Summary

During the hard-fork of the Ethereum chain on block 1,920,000 the ethers (ETH) from The DAO and it's children were moved into a Withdrawal Contract at [0xbf4ed7b27f1d666546e30d74d50d173d20bca754](https://etherscan.io/address/0xbf4ed7b27f1d666546e30d74d50d173d20bca754#code).

The DAO token holders (DTH) could then convert their The DAO tokens (DAO) back to ETH for a refund at a rate of 100 DAO = 1 ETH. When DTHs convert their DAOs into ETH, they transfer the DAO balances from their account to the Withdrawal Contract and the Withdrawal Contract then sends the equivalent ETH to the DTH's account.

The script in this repository queries the blockchain for all The DAO `CreatedToken` events and `Transfer` events to compile a list of all addresses that could possibly be holding DAO balances. The script then finds the DAO balance of each address just prior to the hard fork at block 1,919,999 and at block 2,082,500 (Aug-16-2016 12:24:57 PM +UTC).

The results are being analysed currently in the [theDAOETHTokenBalance_20160818_094448UTC_balance.xlsx](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/theDAOETHTokenBalance_20160818_094448UTC_balance.xlsx) spreadsheet.

Summary of results:
* The number of accounts that have held DAOs at either of the blocks 1,919,999 and/or 2,082,500 = 22,546. This is the number of non-zero lines in the Balances worksheet in the spreadsheet.
* Total DAO balance at block 1,919,999 = 1,153,816,598.70
* Total DAO balance at block 2,082,500 = 1,153,816,598.70
  * DAO balance of the Withdrawal Contract at block 2,082,500 = 916,307,167.97 (79.42%)
  * DAOs that have not been converted into ETHs at block 2,082,500 = 237,509,430.73	(20.58%)



<br />

---

# Details

## Output
Running the script [getTheDAOETHTokenBalance](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/getTheDAOETHTokenBalance) produces the following result files:

* [theDAOETHTokenBalance_20160818_094448UTC_all.txt](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/theDAOETHTokenBalance_20160818_094448UTC_all.txt)
* [theDAOETHTokenBalance_20160818_094448UTC_creation.txt](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/theDAOETHTokenBalance_20160818_094448UTC_creation.txt)
* [theDAOETHTokenBalance_20160818_094448UTC_transfer.txt](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/theDAOETHTokenBalance_20160818_094448UTC_transfer.txt)
* [theDAOETHTokenBalance_20160818_094448UTC_balance.txt](https://github.com/bokkypoobah/TheDAOETHTokenBalance/blob/master/theDAOETHTokenBalance_20160818_094448UTC_balance.txt)

## Check
The bottom of the _balances.txt file has the following statistics:

    Stats	nonZeroAccounts	22546
    Stats	daosPreHardForkTotal	11538165987023813647269888	1153816598.7023813724517822
    Stats	daosCurrentTotal	11538165987024618953637888	1153816598.7024619579315186
    
Running the following commands on the `geth` command line:

    > var theDAOABIFragment=[{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"type":"function"}];
    undefined
    > var theDAO = web3.eth.contract(theDAOABIFragment).at(theDAOAddress);
    undefined
    > var totalSupply=theDAO.totalSupply(1919999);
    undefined
    > totalSupply/1e16
    1153816598.702467
    
The DAO's total supply matches the `daosPreHardForkTotal` and `daosCurrentTotal` statistics above.
