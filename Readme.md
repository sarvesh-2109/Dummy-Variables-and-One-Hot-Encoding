# Dummy Variables & One Hot Encoding

This repository contains a demonstration of how to use dummy variables and one-hot encoding for categorical data in machine learning models. The dataset used is related to car prices and includes features like car model, mileage, and age. The project shows how to handle categorical variables using pandas and scikit-learn libraries.

## Output


https://github.com/sarvesh-2109/Dummy-Variables-and-One-Hot-Encoding/assets/113255836/cc06a337-4778-4107-8688-07c0e34703c3



## Table of Contents
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
  - [Using Dummy Variables](#using-dummy-variables)
  - [Using One-Hot Encoding with scikit-learn](#using-one-hot-encoding-with-scikit-learn)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Dataset

The dataset `carprices.csv` contains the following columns:
- `Car Model`: The model of the car.
- `Mileage`: The mileage of the car.
- `Age(yrs)`: The age of the car in years.
- `Sell Price($)`: The selling price of the car.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/sarvesh-2109/Dummy-Variables-and-One-Hot-Encoding.git
   ```

2. Change into the directory:
   ```bash
   cd Dummy-Variables-and-One-Hot-Encoding
   ```

3. Install the required packages:
   ```bash
   pip install pandas numpy scikit-learn
   ```

## Usage

### Using Dummy Variables

1. Load the dataset:
   ```python
   import pandas as pd
   data = pd.read_csv('carprices.csv')
   ```

2. Create dummy variables:
   ```python
   dummies = pd.get_dummies(data['Car Model']).astype(int)
   ```

3. Merge the dummy variables with the original dataset:
   ```python
   merged = pd.concat([data, dummies], axis='columns')
   final = merged.drop(['Car Model', 'Mercedez Benz C class'], axis='columns')
   ```

4. Train the model:
   ```python
   from sklearn.linear_model import LinearRegression
   model = LinearRegression()
   X = final.drop('Sell Price($)', axis='columns')
   y = final['Sell Price($)']
   model.fit(X, y)
   ```

5. Make predictions:
   ```python
   model.predict([[45000, 4, 0, 0]])  # Mercedez Benz C class
   model.predict([[86000, 7, 0, 1]])  # BMW X5
   ```

### Using One-Hot Encoding with scikit-learn

1. Load the dataset:
   ```python
   from sklearn.preprocessing import LabelEncoder, OneHotEncoder
   import pandas as pd
   df = pd.read_csv('carprices.csv')
   ```

2. Encode the categorical variable:
   ```python
   le = LabelEncoder()
   df['Car Model'] = le.fit_transform(df['Car Model'])
   ```

3. Apply one-hot encoding:
   ```python
   ohe = OneHotEncoder(sparse=False, dtype=int)
   X_ohe = ohe.fit_transform(df[['Car Model']])
   X = pd.concat([pd.DataFrame(X_ohe, columns=ohe.get_feature_names_out(['Car Model'])), df[['Mileage', 'Age(yrs)']].reset_index(drop=True)], axis=1)
   ```

4. Train the model:
   ```python
   model = LinearRegression()
   model.fit(X, y)
   ```

5. Make predictions:
   ```python
   model.predict([[0, 0, 1, 45000, 4]])  # Mercedez Benz C class
   model.predict([[0, 1, 0, 86000, 7]])  # BMW X5
   ```

## Results

- The model trained using dummy variables and one-hot encoding can predict car prices based on the features provided.
- The accuracy of the model can be assessed using the `model.score` method.

## Contributing

Contributions are welcome! Please create an issue to discuss your idea, or fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
