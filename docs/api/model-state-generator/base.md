# Model State Generator Base Classes

## FeatureBase

Base abstract class for all features in the system.

```python
class FeatureBase(ABC):
    """
    Abstract base class for all features.

    :param name: Name of the feature
    :param description: Description of what the feature represents
    :param kwargs: Additional keyword arguments for feature configuration
    """

    def __init__(self, name: str, description: str, **kwargs: Any) -> None:
        self.name = name
        self.description = description
```

### Methods

#### get_name()

```python
def get_name(self) -> str:
    """
    Returns the feature name.

    :return: Name of the feature
    """
```

#### get_description()

```python
def get_description(self) -> str:
    """
    Returns the feature description.

    :return: Description of the feature
    """
```

## DatabaseFeatureBase

Base class for features that are retrieved directly from the database.

```python
class DatabaseFeatureBase(FeatureBase):
    """
    Base class for features sourced from database.

    :param name: Name of the database feature
    :param description: Description of what the feature represents
    :param kwargs: Additional configuration parameters
    """
```

### Methods

#### get_data()

```python
@abstractmethod
def get_data(self) -> Any:
    """
    Retrieves feature data from the database.

    :return: Feature data in the appropriate format
    :raises: NotImplementedError when not implemented by child class
    """
```

## ComputedFeatureBase

Base class for features that are computed from other features.

```python
class ComputedFeatureBase(FeatureBase):
    """
    Base class for computed features.

    :param name: Name of the computed feature
    :param description: Description of what the feature represents
    :param kwargs: Additional computation parameters
    """
```

### Methods

#### compute_feature()

```python
@abstractmethod
def compute_feature(self, data: Any) -> Any:
    """
    Computes the feature value from input data.

    :param data: Input data required for feature computation
    :return: Computed feature values
    :raises: NotImplementedError when not implemented by child class
    """
```

## Usage Example

```python
from src.model_state_generator.features.feature_base import ComputedFeatureBase

class RSIFeature(ComputedFeatureBase):
    def __init__(self, period: int = 14):
        super().__init__(
            name=f"RSI_{period}",
            description=f"{period}-period Relative Strength Index"
        )
        self.period = period

    def compute_feature(self, data: pd.DataFrame) -> pd.Series:
        return talib.RSI(data['close'], timeperiod=self.period)
```
