# FactSet
This page provides all information on the data we are sourcing from FactSet.

---

## FactSet Futures OHLCVO
[Source code in GitHub repository](https://github.com/Hawk-Center/data-engineering/blob/main/pipeline/sources/factset_futures_ohlcvo.py)

```
Process runs at 11:00 PM UTC. 
Should be available in BigQuery <1 minute after. 
Data should be available in GCS at ~11:30pm UTC.
```

Sources 1-day `Open`, `High`, `Low`, `Close`, `Volume`, and `Open Interest` data for Futures from the `FactSet Formula`
endpoint.

Currently, sources data for the following Futures:

```
(HAWK-ID) TICKER: CONTRACT-NAME
(20000) CL00-USA: Crude Oil Futures
(20001) BRN00-IFEU: Brent Crude Oil Futures
(20002) GC00-USA: Gold Futures
(20003) SI00-USA: Silver Futures
(20004) NG00-USA: Natural Gas Futures
(20005) TU00-USA: 2-Year U.S. Treasury Note Futures
(20006) FV00-USA: 5-Year U.S. Treasury Note Futures
(20007) TY00-USA: 10-Year U.S. Treasury Note Futures
(20008) JBT00-OSE: Japanese Government Bond Futures
(20009) JGBS00-OSE: Japanese Government Bond Futures (Alternate)
(20010) FGBS00-EUR: Euro-Bund Futures
(20011) FGBM00-EUR: Euro-Bobl Futures
(20012) FGBL00-EUR: Euro-Schatz Futures
(20013) RLI00-IFEU: RBOB Gasoline Futures
(20014) ES00-USA: E-mini S&P 500 Futures
(20015) NQ00-USA: E-mini Nasdaq-100 Futures
(20016) FESX00-EUR: Euro Stoxx 50 Futures
(20017) Z00-IFEU: Euro FX Futures
(20018) NIK22500-OSE: Nikkei 225 Futures
(20019) RMB00-USA: Renminbi Futures
(20020) EC00-USA: Euro FX Futures
(20021) JY00-USA: Japanese Yen Futures
(20022) SFC00-USA: Softs Futures (Various Commodities)
(20023) BP00-USA: British Pound Futures
```

See the [FactSet Formula API](https://developer.factset.com/api-catalog/formula-api) documentation for more information.

---

## FactSet Futures Snapshot
[Source code in GitHub repository](https://github.com/Hawk-Center/data-engineering/blob/main/pipeline/sources/factset_futures_snapshot.py)


```
Runs at 8:29 PM UTC. 
Should be available in BigQuery <1 minute after. 
GCS access is not yet available for this data.
```

Sources current `Open`, `High`, `Low`, `Close`, `Bid`, `Ask`, and `Cvol` for Futures from the `FactSet Exchange Datafeed Snapshot API` endpoint.

Currently, sources data for the following Futures:

```
(HAWK-ID) TICKER: CONTRACT-NAME
(20000) CL00-USA: Crude Oil Futures
(20001) BRN00-IFEU: Brent Crude Oil Futures
(20002) GC00-USA: Gold Futures
(20003) SI00-USA: Silver Futures
(20004) NG00-USA: Natural Gas Futures
(20005) TU00-USA: 2-Year U.S. Treasury Note Futures
(20006) FV00-USA: 5-Year U.S. Treasury Note Futures
(20007) TY00-USA: 10-Year U.S. Treasury Note Futures
(20008) JBT00-OSE: Japanese Government Bond Futures
(20009) JGBS00-OSE: Japanese Government Bond Futures (Alternate)
(20010) FGBS00-EUR: Euro-Bund Futures
(20011) FGBM00-EUR: Euro-Bobl Futures
(20012) FGBL00-EUR: Euro-Schatz Futures
(20013) RLI00-IFEU: RBOB Gasoline Futures
(20014) ES00-USA: E-mini S&P 500 Futures
(20015) NQ00-USA: E-mini Nasdaq-100 Futures
(20016) FESX00-EUR: Euro Stoxx 50 Futures
(20017) Z00-IFEU: Euro FX Futures
(20018) NIK22500-OSE: Nikkei 225 Futures
(20019) RMB00-USA: Renminbi Futures
(20020) EC00-USA: Euro FX Futures
(20021) JY00-USA: Japanese Yen Futures
(20022) SFC00-USA: Softs Futures (Various Commodities)
(20023) BP00-USA: British Pound Futures
```

See the [FactSet Exchange Datafeed Snapshot API](https://developer.factset.com/api-catalog/exchange-datafeed-snapshot-api-symbol-list) documentation for more information.

