# Getting Started

## Prerequisites

Before you begin, ensure you have the following installed:

- Python 3.10 or higher
- Docker and Docker Compose
- Poetry (Python dependency management)
- Git

## Initial Setup

1. Clone the repository:

```bash
git clone https://github.com/Hawk-Center/production-engineering.git
cd production-engineering
```

2. Install dependencies using Poetry:

``` bash
poetry install
```

3. Set up Google Cloud credentials:

- Download your service account JSON file
- Rename it to `service_account.json`
- Place it in the project root directory

## Configuration

### Environment Setup

1. Create a local environment file:

```bash
cp .env.example .env
```

```bash
GOOGLE_APPLICATION_CREDENTIALS=/app/service_account.json
MOSEK_LICENSE_PATH=/opt/mosek/mosek.lic # If using MOSEK optimizer
```

### Model Configuration

Models are configured via YAML files located in `src/model_state_generator/configs/`. Each model requires:

- Feature definitions
- Data source specifications
- Model parameters

Example configuration:

```yaml
model_state_name: example_model
pod_name: hawk_global_futures
universe_id: hawk_global_futures_universe
bucket_name: your-gcs-bucket
interval: 1d
start_date: "2010-01-01"
```

## Running the Pipeline

### 1. Build Docker Images

Build all required containers:

```bash
docker-compose build
```

### 2. Generate Model States

Run the model state generator:

```bash
docker-compose up trading_models
```

### 3. Execute Trading Models

Run the trading models:

```bash
docker-compose up trading_models
```

### 4. Run Portfolio Simulation

Execute the portfolio simulator:

```bash
docker-compose up simulator
```

### 5. Aggregate Results

Run the model aggregator:

```bash
docker-compose up aggregator
```

## Architecture-Specific Setup

### Apple Silicon (M1/M2)

If running on Apple Silicon, modify the TA-Lib configuration in
`docker/model_state_generator/Dockerfile`:

```dockerfile
./configure --prefix=/usr --build=aarch64-unknown-linux-gnu && \
```

### Linux Systems

Standard configuration should work out of the box:

## Development Workflow

1. Create a new branch for your changes:

```bash
git checkout -b feature/your-feature-name
```

2. Make an empty commit and create a pull request:

```bash
git commit --allow-empty -m "[HAWK-XX] Your feature description"
git push -u origin feature/your-feature-name
```

3. Follow the development guidelines in [CONTIBUTING.md](../CONTRIBUTING.md)

## Troubleshooting

### Common Issues

1. Docker permission errors:

```bash
sudo docker-compose up
```

2. TA-Lib installation issues:

```bash
docker-compose build --no-cache model_state_generator
```

3. Missing dependencies:

```bash
poetry install --no-cache
```

### Getting Help

- Check the logs: `docker-compose logs -f [service_name]`
- Review documentation in the `docs/` directory
- Submit issues through the project's issue tracker

## Next Steps

- Review the [Architecture Overview](architecture.md)
- Explore [Available Models](../trading-models/available-models.md)
- Learn about [Portfolio Simulation](../portfolio-simulation/backtesting.md)
