# Privacy Preserving Machine Learning Demo
### Scenario 1: Encrypting the Patient Data Only

This project shows how machine learning predictions can be made without exposing real patient data. It follows Scenario 1 from the paper "Machine Learning in Precision Medicine to Preserve Privacy via Encryption." The idea is that patient data is encrypted, sent to a server, and the server makes predictions without ever seeing the original values. The code is a simplified version of the method used in the research paper.

This demo uses the Breast Cancer Wisconsin Diagnostic (WDBC) dataset, which contains real medical features measured from tumor cell samples.

## Project Layout

```
CS4371project/
    data/
        wdbc.data
    src/
        dataset.py
        encrypt.py
        model.py
        demo_helper.py
        demo.py
    requirements.txt
    README.md
```

## Tools and Libraries Used

- Python 3
- NumPy
- pandas
- scikit-learn
- TenSEAL (CKKS encryption scheme)

## Installation

Create and activate a virtual environment:

```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Windows:

```
.venv\Scripts\activate
```

## How to Run the Demo

Run the main scenario:

```
python -m src.demo
```

Run the simplified version used for presentations:

```
python -m src.demo_helper
```

## What the Demo Does

1. Loads the WDBC dataset, which contains 30 different diagnostic measurements.
2. Trains a logistic regression model on plaintext data.
3. Encrypts the patient test data using the CKKS scheme.
4. Makes predictions on encrypted data.
5. Compares encrypted predictions to plaintext predictions.

## Example Output

```
Plain Acc: 0.9708
Enc Acc: 0.9667
Plain Time: 0.0005 sec
Enc Time: 1.3414 sec
```

These results show that encrypted predictions stay very close to the normal predictions. They take longer to compute, which is expected when using homomorphic encryption.

## How This Relates to Scenario 1 in the Paper

Scenario 1 is based on input-only encryption. The patient encrypts their data, sends it to the server, and the server performs the model's linear layer on the encrypted values. The server then returns an encrypted prediction that only the patient can decrypt. The model itself is not encrypted.

This project follows the same steps.

## Why Accuracy Drops a Little

The CKKS encryption scheme uses approximate arithmetic. This means that small rounding errors and numerical approximations can slightly change the output. The accuracy drop in this demo is very small and shows that encrypted prediction can still work well.

## Key Points Learned

- Machine learning can run on encrypted data.
- The server never learns the real patient values.
- Encrypted prediction is slower than normal prediction.
- Accuracy stays almost the same.
- Scenario 1 is practical for medical privacy because only the inputs need to be encrypted.

## References

- Machine Learning in Precision Medicine to Preserve Privacy via Encryption
- Gentry, C. (2009). Fully Homomorphic Encryption Using Ideal Lattices.
- Cheon et al. (2017). Homomorphic Encryption for Arithmetic of Approximate Numbers (CKKS).
- Breast Cancer Wisconsin Diagnostic Dataset (WDBC), UCI Machine Learning Repository.