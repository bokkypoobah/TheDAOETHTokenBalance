# TheDAOETHTokenBalance

Scripts and data to compute the balances of The DAO token holders on the hard-forked Ethereum chain.

<br />

---

# Summary

During the hard-fork of the Ethereum chain on block 1,920,000 the ethers (ETH) from The DAO and it's children were moved into a withdrawal contract at [0xbf4ed7b27f1d666546e30d74d50d173d20bca754](https://etherscan.io/address/0xbf4ed7b27f1d666546e30d74d50d173d20bca754#code).

The DAO token holders (DTH) could then convert their The DAO tokens (DAO) back to ETH for a refund at a rate of 100 DAO = 1 ETH. This analysis looks at the statistics of the number of accounts that have converted the DAOs into ETHs.

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
