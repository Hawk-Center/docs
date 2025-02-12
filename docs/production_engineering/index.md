# Hawk Production Engineering Documentation

## Overview

- [Architecture](overview/architecture.md)
- [Pipeline Workflow](overview/pipeline.md)
- [Key Components](overview/components.md)
- [Getting Started](overview/getting-started.md)

## Model State Generation

- Feature Engineering Pipeline
  - [Feature Engineering Overview](model-state-generation/feature-engineering.md)
  - Technical Indicators
  - Data Sources
  - Custom Features
- [Configuration](model-state-generation/configuration.md)
  - YAML Structure
  - Feature Definitions
  - Runtime Modes (EOD/Intraday)
- [Data Flow](model-state-generation/data-flow.md)
  - Input Data Requirements
  - Output Format
  - GCS Storage Structure

## Trading Models

- [API Reference](production_engineering/api/trading-models.md)
- Available Models
  - EMA Cross Strategies
  - RSI Strategy
  - Adding New Models
- Model Configuration
  - YAML Configuration
  - Model Parameters
  - State Management

## Portfolio Simulation

- [Backtesting Framework](portfolio-simulation/backtesting.md)
  - Data Requirements
  - Performance Metrics
  - Risk Metrics
- [Portfolio Management](portfolio-simulation/management.md)
  - Position Sizing
  - Risk Management
  - Rebalancing Logic
- [Results Analysis](portfolio-simulation/analysis.md)
  - Performance Reports
  - Risk Analysis
  - Visualization

## Model Aggregation

- [Portfolio Optimization](model-aggregation/optimization.md)
  - Modern Portfolio Theory Implementation
  - MOSEK Integration
  - Optimization Parameters
- [Weight Allocation](model-aggregation/weight-allocation.md)
  - Model Weighting Strategies
  - Risk Constraints
  - Rebalancing Rules

## Developer Guide

- [Setup and Installation](developer-guide/setup.md)
- [Environment Configuration](developer-guide/setup.md#environment-configuration)
- [Development Workflow](developer-guide/workflow.md)
- [Testing Framework](developer-guide/testing.md)
- [Deployment Process](developer-guide/deployment.md)

## API Reference

- [Model State Generator API](production_engineering/api/model-state-generator.md)
- [Trading Model Base Classes](production_engineering/api/trading-models.md)
- [Portfolio Simulator API](production_engineering/api/portfolio-simulator.md)
- [Model Aggregator API](production_engineering/api/model-aggregator.md)
- [Common Utilities](production_engineering/api/common.md)

## Operational Guide

- [Production Pipeline](operations/pipeline.md)
  - Daily Operations
  - Monitoring
  - Alerting
- [Troubleshooting](operations/troubleshooting.md)
  - Common Issues
  - Debug Procedures
  - Logging System
- [Performance Optimization](operations/performance.md)
  - Bottleneck Analysis
  - Scaling Considerations

## Research Extensions

- Adding New Features
- Implementing New Models
- Custom Optimization Strategies
- Backtesting Methodologies
