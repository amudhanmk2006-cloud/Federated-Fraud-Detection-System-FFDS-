import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

banks = [
    (np.array([[100,1],[500,0],[50,1],[900,0]]),[1,0,1,0]),
    (np.array([[200,1],[700,0],[80,1],[600,0]]),[1,0,1,0])
]

models = []
for X,y in banks:
    m = RandomForestClassifier(n_estimators=5)
    m.fit(X,y)
    models.append(m)

X_test = [[150,1],[800,0]]
pred = [round(np.mean([m.predict(X_test)[i] for m in models]))
        for i in range(2)]

print("Fraud Predictions:", pred)
