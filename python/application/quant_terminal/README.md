# 0x API: DeFi Quant Terminal
This application uses the 0x API to produce a mock Uniswap pool which allows end-users to stress test
the limitations of a Uniswap pool setup using live price feeds from [0x API](https://0x.org); for backend setup, see [notebook](https://github.com/defipy-devs/uniswappy/notebooks/quant_terminal.ipynb) 

## Live link to application
Click [dashboard.defipy.org](https://dashboard.defipy.org/) for live link

## Local Installation 

Install project requirements:
```
> git clone https://github.com/defipy-devs/uniswappy
> pip install -r requirements.txt

```

Next, install Uniswappy python package: 
```
> pip install .
```

or 

```
> pip install uniswappy
```

## Run application locally  

```
> bokeh serve --show python/application/quant_terminal/bokeh_server.py
```
### Once the process is running, you need to kill it and restart to apply new changes

First check what the process ID is for the port you're running on (default is 5006):
```
> lsof -ti:5006
``` 
Then kill that process (pid is the output of the previous command)
```
> kill -9 pid
``` 

## DeFiPy ETHDenver BUIDL week additions
* **[QuantTerminal.py](https://github.com/defipy-devs/uniswappy/blob/ethdenver/python/prod/simulate/QuantTerminal.py)**:
    * QuantTerminal Simulator class for BUIDL week; applies the 0x API to produce a mock Uniswap pool to 
      allow end-users to stress test the limitations of a Uniswap pool setup using live price 
      feeds from 0x API
* **[API0x.py](https://github.com/defipy-devs/uniswappy/blob/ethdenver/python/prod/utils/client/API0x.py)**
    * 0x API class which works with Chain0x data class for all necessary API relevant data
* **[Chain0x.py](https://github.com/defipy-devs/uniswappy/blob/ethdenver/python/prod/utils/data/Chain0x.py)**
    * Data class for handling all application data (eg, token contract addresses)
* **[CorrectReserves.py](https://github.com/defipy-devs/uniswappy/blob/ethdenver/python/prod/simulate/CorrectReserves.py)**
    * Applies SolveDeltas class to correct x/y reserve amounts so that price reflects desired input price (see Rebalancing Pool in Technical References section below); 
      in the case for the BUIDL week event, it would be the most recent market price returned from the 0x API 
* **[bokeh_server.py](https://github.com/defipy-devs/uniswappy/blob/ethdenver/python/application/bokeh_server.py)**
    * Front-end Bokeh server to render simulator to end user
		

## Technical References 
 * **Reblancing Pool**: 
     * Math behind rebalancing pool upon price change
     * See [How to Simulate a Uniswap Pool](https://medium.com/@icmoore/simulating-a-liquidity-pool-for-decentralized-finance-6f357ec8564b)
  * **Indexed Liquidity**: 
      * Monitoring profitability of swap positions
      * See [The Uniswap Indexing Problem](https://medium.com/datadriveninvestor/the-uniswap-indexing-problem-8078b8b110fc)
   * **Impermanent Loss**: 
       * How variance impacts impermanent loss
       * See (Eq. 6) [Technical Survey of Impermanent Loss](https://github.com/icmoore/impermanent_loss/blob/main/article.pdf)
 
 
