
### not need threshold metrics
```python
from ts_ad_evaluation import Evaluator
# gt: np.ndarray[int],
# anomaly_score: np.ndarray[float],
# save_path: str
evaluator = Evaluator(gt, anomaly_score, save_path)
evaluator.evaluate(metrics=['best_f1', 'auc', 'r_auc', 'vus'])
evaluator.vis_anomaly_intervals_1()
```

### need threshold (affiliation)
```python
from ts_ad_evaluation import Evaluator
# gt: np.ndarray[int],
# anomaly_score: np.ndarray[float],
# save_path: str
evaluator = Evaluator(gt, anomaly_score, save_path)

# method==spot
# init_energy: np.ndarray[float],
# q: list[float] spot方法超参数
thresholds = evaluator.find_thres(method="spot", init_score=init_energy, q=q)

# method==prior_anomaly_rate
# t: list[float] 假设存在异常的比列：0.1，0.11...
thresholds = evaluator.find_thres(method="prior_anomaly_rate", pAR=t)

# 计算出阈值后进行评估
evaluator.evaluate(metrics=['affiliation'], affiliation=thresholds)
```

