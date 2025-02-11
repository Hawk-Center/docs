# Key Components

## 1. Model State Generator

The Model State Generator is responsible for creating and managing model states by:

- Processing raw market data from BigQuery
- Computing technical indicators using TA-Lib
- Generating feature sets for trading models
- Storing results in Google Cloud Storage (GCS)

### Key Features

- Parallel processing of multiple model configurations
- Support for custom technical indicators
- Configurable via YAML files
- Automated data validation and error handling

## 2. Trading Models

Trading models consume model states to generate trading signals. Current implementations include:

- EMA Cross Strategies (8/32, 16/64, 32/128, 64/256)
- RSI Strategy (14-period)

### Features

- Version-controlled model implementations
- Configurable parameters via YAML
- Real-time and batch processing capabilities
- Standardized output format for portfolio simulation

## 3. Portfolio Simulator

The Portfolio Simulator evaluates trading model performance by:

- Backtesting model signals
- Computing performance metrics
- Analyzing risk characteristics
- Generating performance reports

### Key Capabilities

- Historical performance analysis
- Risk metrics calculation
- Transaction cost modeling
- Performance attribution

## 4. Model Aggregator

The Model Aggregator optimizes portfolio allocation by:

- Combining signals from multiple models
- Optimizing weights using MOSEK
- Managing risk constraints
- Generating final portfolio insights

### Features

- Modern Portfolio Theory implementation
- Risk-adjusted optimization
- Dynamic weight rebalancing
- Multi-model signal aggregation

## 5. Infrastructure Components

### Docker Containers

- Isolated execution environments for each component
- Consistent deployment across environments
- Simplified dependency management
- Scalable architecture

### Airflow Integration

- Automated pipeline scheduling
- Dependency management between tasks
- Error handling and retries
- Pipeline monitoring and logging

### Storage

- Google Cloud Storage for model states and insights
- BigQuery for raw market data
- Local storage for temporary files
- Efficient data format (Parquet/JSON)
