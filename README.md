from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# データ読み込み
data = load_iris()
X = data.data
y = data.target

# 分ける
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# AI作成
model = RandomForestClassifier()

# 覚えさせる
model.fit(X_train, y_train)

# テスト
score = model.score(X_test, y_test)

print("正解率:", score)
# ai-study
