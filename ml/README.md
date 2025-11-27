# ML Training Documentation

This document contains the training logs and notebook output for the SageMaker DeepAR crowd density prediction model.

## Model Overview

- **Algorithm**: Amazon SageMaker DeepAR (Time Series Forecasting)
- **Task**: Predict crowd density for event venues
- **Data Source**: S3 bucket (`crowd-hackathon-bucket`)

## Training Configuration

### Hyperparameters

| Parameter               | Value                   |
| ----------------------- | ----------------------- |
| Epochs                  | 100                     |
| Mini Batch Size         | 64                      |
| Learning Rate           | 0.004                   |
| Context Length          | 30 (5-minute intervals) |
| Prediction Length       | 78 (~6.5 hours)         |
| Number of Layers        | 3                       |
| Number of Cells         | 120                     |
| Dropout Rate            | 0.15                    |
| Early Stopping Patience | 15                      |

### Dataset

- **Frequency**: 5-minute intervals
- **Training Window**: First 10 hours per day (120 points)
- **Test Window**: Last 6.5 hours per day (78 points)
- **Total Time Series**: 14 days
- **Features**: Density, temperature, rain, wind speed, bus arrival, day phase indicators

## Data Preprocessing

1. Load data from S3 CSV file
2. Parse datetime index
3. Split into 16-hour daily segments (06:00-22:00)
4. Create train/test splits
5. Export to JSON format for DeepAR

## Model Architecture

DeepAR uses an autoregressive recurrent neural network to model the joint probability distribution of all time series. Key components:

- **Encoder**: Processes historical context (30 time steps)
- **Decoder**: Generates probabilistic forecasts
- **Likelihood**: Student-t distribution for robust predictions

## Training Results

The model achieved early stopping with best loss around epoch 45-50. Final training metrics showed consistent improvement with the loss decreasing from ~10.6 to ~5.7.

## Usage

The trained model is deployed as a SageMaker endpoint and invoked by the Lambda function with the following payload format:

```json
{
  "instances": [
    {
      "start": "2025-09-01 06:00",
      "target": [],
      "cat": [0]
    }
  ],
  "configuration": {
    "num_samples": 50,
    "output_types": ["quantiles"],
    "quantiles": ["0.1", "0.5", "0.9"]
  }
}
```

## Related Files

- `Backend/main.py` - Lambda function that invokes this model
- `Frontend/src/App.jsx` - Dashboard that displays predictions

## References

- [Amazon SageMaker DeepAR Documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/deepar.html)
