# Kalman_Filter

### 1. 예측 단계 (Prediction / Time Update)
시스템 모델을 바탕으로 다음 상태와 오차 공분산을 예측합니다.

$$
\hat{x}_{k}^{-} = A\hat{x}_{k-1} + Bu_{k-1}
$$

$$
P_{k}^{-} = AP_{k-1}A^{T} + Q
$$

* $\hat{x}_{k}^{-}$ : 추정된 예측 상태 (Prior State Estimate)
* $P_{k}^{-}$ : 추정된 예측 오차 공분산 (Prior Error Covariance)
* $A$ : 상태 전이 행렬 (State Transition Matrix)
* $B$ : 제어 입력 행렬 (Control Input Matrix)
* $u_{k-1}$ : 제어 입력 (Control Input)
* $Q$ : 프로세스 노이즈 공분산 (Process Noise Covariance)

---

### 2. 추정 및 갱신 단계 (Update / Measurement Update)
센서의 측정값을 반영하여 더 정확한 상태로 보정합니다.

**[칼만 이득 계산]** 
$$
K_{k} = P_{k}^{-}H^{T}(HP_{k}^{-}H^{T} + R)^{-1}
$$

**[상태 추정치 갱신]**

$$
\hat{x}_{k} = \hat{x}_{k}^{-} + K_{k}(z_{k} - H\hat{x}_{k}^{-})
$$

**[오차 공분산 갱신]**
$$
P_{k} = (I - K_{k}H)P_{k}^{-}
$$

* $K_{k}$ : 칼만 이득 (Kalman Gain)
* $H$ : 측정 행렬 (Measurement Matrix)
* $R$ : 측정 노이즈 공분산 (Measurement Noise Covariance)
* $z_{k}$ : 실제 측정값 (Measurement)
* $I$ : 단위 행렬 (Identity Matrix)
