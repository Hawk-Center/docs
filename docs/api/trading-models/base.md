# Trading Models Base Classes

## TradingModelBase

Abstract base class for all trading models in the system.

```python
class TradingModelBase(ABC):
    """
    Abstract base class for all trading models.

    :param model_info: Trading model metadata
    :param model_state: Pre-computed feature data for the model
    :param runtime_mode: Execution mode (EOD/INTRADAY)
    """

    def __init__(
        self,
        model_info: TradingModelInfo,
        model_state: pd.DataFrame,
        runtime_mode: RuntimeMode
    ) -> None:
        self.model_info = model_info
        self.model_state = model_state
        self.runtime_mode = runtime_mode
```

### Core Methods

#### generate_insights()

```python
@abstractmethod
def generate_insights(self) -> ModelInsights:
    """
    Generates trading insights from model state data.

    :return: Collection of trading insights
    :raises: NotImplementedError when not implemented by child class
    """
```

## Strategy Implementation Example

Here's how to implement a simple moving average crossover strategy:

```python
class EMACrossStrategy(TradingModelBase):
    """
    Moving average crossover trading strategy.

    :param fast_period: Period for fast moving average
    :param slow_period: Period for slow moving average
    """

    def __init__(
        self,
        model_info: TradingModelInfo,
        model_state: pd.DataFrame,
        fast_period: int = 8,
        slow_period: int = 32
    ) -> None:
        super().__init__(model_info, model_state, RuntimeMode.EOD)
        self.fast_period = fast_period
        self.slow_period = slow_period

    def generate_insights(self) -> ModelInsights:
        """
        Generates trading signals based on EMA crossovers.

        :return: Collection of trading insights
        """
        fast_ema = self.model_state[f'ema_{self.fast_period}']
        slow_ema = self.model_state[f'ema_{self.slow_period}']

        # Generate crossover signals
        signal = np.where(
            fast_ema > slow_ema,
            PositionType.LONG,
            PositionType.SHORT
        )

        # Create insights
        insights = {}
        for ticker in self.model_state['ticker'].unique():
            insights[ticker] = SecurityInsight(
                ticker=ticker,
                position_type=signal[-1],
                weight=1.0
            )

        return ModelInsights(
            model_info=self.model_info,
            insights=insights,
            insight_date=datetime.now()
        )
```

## Configuration

Trading models are configured through YAML files:

```yaml
trading_model_name: ema_cross_8_32
model_state_name: ema_cross_features
runtime_mode: EOD
parameters:
  fast_period: 8
  slow_period: 32
```

## Usage Example

```python
# Load model state from GCS
model_state = pd.read_parquet('gs://bucket/model_states/ema_cross_features.parquet')

# Create model info
model_info = TradingModelInfo(
    trading_model_name="ema_cross_8_32",
    model_state_name="ema_cross_features",
    runtime_mode=RuntimeMode.EOD,
    bucket_name="your-bucket",
    pod_name="your-pod",
    model_class="EMACrossStrategy"
)

# Initialize and run model
model = EMACrossStrategy(model_info, model_state)
insights = model.generate_insights()
```

For reference to types and enums, see:

```markdown:docs/api/common/types.md
startLine: 1
endLine: 97
```

```markdown:docs/api/common/enums.md
startLine: 1
endLine: 56
```
