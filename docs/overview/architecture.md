# System Architecture

## Overview

The Hawk Production Engineering system consists of four main components that work together in a pipeline:

```mermaid
graph LR

    A[Model State Generator] --> B[Trading Models]
    B --> C[Portfolio Simulator]
    C --> D[Model Aggregator]
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#fbb,stroke:#333,stroke-width:2px
    style D fill:#bfb,stroke:#333,stroke-width:2px
```

## Component Details

### 1. Model State Generator

```mermaid
graph TD
    A[Raw Market Data from BigQuery] --> B[Feature Engineering]
    B --> C[Technical Indicators TA-Lib]
    B --> D[Custom Features]
    C --> E[Model State]
    D --> E
    E --> F[Parquet to GCS Storage]
```

- Ingests raw market data
- Computes technical indicators (EMA, RSI, etc.)
- Generates feature sets for each model
- Stores results in Google Cloud Storage

### 2. Trading Models

```mermaid
graph LR
    A[Model States] --> B[EMA Cross Models]
    A --> C[RSI Models]
    B --> D[Portfolio Insights]
    C --> D
    D --> E[Parquet to GCS Storage]
```

- Consumes model states
- Implements trading strategies
- Generates position signals
- Supports multiple model types:
  - EMA Cross Strategies
  - RSI Strategy
  - Others ?? (To be added, i.e kernel regression, hurst exponent, committment of traders, binary classifiers, reversal indicators, etc.)

### 3. Portfolio Simulator

```mermaid
graph LR
    A[Model Insights] --> B[hawk_backtester]
    B --> C[Timeseries of Historical Performance]
    B --> D[Performance Metrics]

```

### 4. Model Aggregator

```mermaid
graph TD
    A[Simulated Model Timeseries] --> B[Portfolio Optimization Problem]
    B --> C[MOSEK Solver]
    C --> D[Model Weight Allocations]
    D --> E[Combined Portfolio Insights]
```

- Implements portfolio optimization using MOSEK -- Finds optimal risk-adjusted portfolio
- Aggregates signals from multiple models using historical performance & correlations
- Generates final portfolio insights as a linear combination of model insights

## Data Flow

```mermaid
sequenceDiagram
    participant BQ as BigQuery
    participant MSG as Model State Generator
    participant GCS as Google Cloud Storage
    participant TM as Trading Models
    participant PS as Portfolio Simulator
    participant MA as Model Aggregator
    BQ->>MSG: Query Raw Dataset Features
    MSG->>GCS: Store Feature Sets
    GCS->>TM: Read Feature Sets
    TM->>GCS: Store Model Insights
    GCS->>PS: Read Insights
    PS->>GCS: Store Performance Timeseries
    GCS->>MA: Read Performance Timeseries
    MA->>GCS: Store Aggregated Insights
```

## Deployment Architecture

```mermaid
graph TD
subgraph Docker Containers
    A[Model State Generator Container]
    B[Trading Models Container]
    C[Portfolio Simulator Container]
    D[Model Aggregator Container]
    A -->|Triggers| B
    B -->|Triggers| C
    C --> |Triggers| D

    end
subgraph Storage
    E[Google Cloud Storage]
    G[BigQuery Database]
    end
subgraph Orchestration
    F[Airflow DAGs]
    end
    F -->|Triggers| A
    A -->|Writes| E
    B -->|Reads/Writes| E
    C -->|Reads/Writes| E
    D -->|Reads/Writes| E
    A -->|Reads| G
```

## Current Services

| Service | Purpose | Key Technologies |
|---------|----------|-----------------|
| Model State Generator | Feature engineering and state preparation | Python, TA-Lib |
| Trading Models | Strategy implementation and signal generation | Python |
| Portfolio Simulator | Performance analysis and backtesting | Python, hawk-backtester |
| Model Aggregator | Portfolio optimization and weight allocation | Python, MOSEK |
