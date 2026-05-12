# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# Date: 28/04/2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_excel('/content/supermarket_10years.xlsx')

resampled_data = data.groupby('Year')['Sales_Amount'].sum().reset_index()

years = resampled_data['Year'].tolist()
sales = resampled_data['Sales_Amount'].tolist()

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, sales)]

n = len(years)

b = (n * sum(xy) - sum(sales) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(sales) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]

print(f"Linear Trend Equation: y = {a:.2f} + {b:.2f}x")

resampled_data['Linear Trend'] = linear_trend

resampled_data.set_index('Year', inplace=True)

resampled_data['Sales_Amount'].plot(kind='line', marker='o')
resampled_data['Linear Trend'].plot(kind='line', linestyle='--')

plt.title('Linear Trend Estimation (Least Square Method)')
plt.xlabel('Year')
plt.ylabel('Total Sales Amount')

plt.legend([
    'Actual Sales',
    f'Linear Trend: y={a:.2f}+{b:.2f}x'
])

plt.grid(True)
plt.tight_layout()
plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_excel('/content/supermarket_10years.xlsx')

resampled_data = data.groupby('Year')['Sales_Amount'].sum().reset_index()

years = resampled_data['Year'].tolist()
sales = resampled_data['Sales_Amount'].tolist()

X = [i - years[len(years) // 2] for i in years]

x2 = [i ** 2 for i in X]
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]

xy = [i * j for i, j in zip(X, sales)]
x2y = [i * j for i, j in zip(x2, sales)]

coeff = [
    [len(X), sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [sum(sales), sum(xy), sum(x2y)]

A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A, B)

a_poly, b_poly, c_poly = solution

poly_trend = [
    a_poly + b_poly * X[i] + c_poly * (X[i] ** 2)
    for i in range(len(years))
]

print(f"Polynomial Trend Equation: y = {a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

resampled_data['Polynomial Trend'] = poly_trend

resampled_data.set_index('Year', inplace=True)

resampled_data['Sales_Amount'].plot(kind='line', marker='o')

resampled_data['Polynomial Trend'].plot(kind='line', marker='o')

plt.title('Polynomial Trend Estimation - Degree 2 (Least Square Method)')

plt.xlabel('Year')
plt.ylabel('Sales Amount')

plt.legend([
    'Actual Sales',
    f'Poly Trend: y={a_poly:.2f}+{b_poly:.2f}x+{c_poly:.2f}x²'
])

plt.grid(True)
plt.tight_layout()
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="1002" height="616" alt="image" src="https://github.com/user-attachments/assets/1c3f4296-baf3-416f-980c-8bbc2c6e6c6c" />


B- POLYNOMIAL TREND ESTIMATION
<img width="1002" height="610" alt="image" src="https://github.com/user-attachments/assets/e7777e92-68e3-49ed-bb4f-0dfe8b3fab49" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
