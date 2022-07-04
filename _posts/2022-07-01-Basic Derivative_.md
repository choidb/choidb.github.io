# 기초 미분 (Basic Derivative)  

**목차**  
[1. 미분](#1-미분derivative)  
[2. 편미분](#2-편미분-partial-derivative)  
[3. Chain rule](#3-chain-rule)  
[4. 경사하강법](#4-경사하강법gradient-descent)


---
* Contents
  1. 최적화와 미분의 관계
  2. 미분, 편미분, Chain Rule의 차이
  3. 도함수를 파이썬으로 직접 구현하거나 scipy 라이브러리를 활용

>
* Keywards
  * 미분
  * 편미분
  * Chain Rule
  * scipy 라이브러리

---


## 1. 미분(Derivative)

* 특정한 파라미터 값 (input, x)에 대해서 나오는 결과값(output, y)이 변화하는 정도를 (0에 가까운 부분을 찾기 위해) 계산하는 것.
* x를 넣었을 때, y 값을 예측하는 선형 모델 표현:
  * y = a + bX
  * 여기서 a 는 y-절편 (y-intercept), b 는 기울기 (slope) 
* 선형회귀모델의 경우 오차 함수는 보통 Mean Squared Error 사용
* 오차 함수를 최소화하는 a, b를 구하기 위해서 우리는 미분을 사용  

  * $f'(x) = {f(x + \Delta x) - f(x) \over \Delta x}$, $\Delta x \rightarrow 0$
* 실제로 0으로 나눌 수는 없기 때문에 보통  1e−5  을 사용하며 numerical method 이라고 표현함
* numerical method에서 좀 더 정확한 측정을 위해 $f(x + \Delta x) - f(x - \Delta x) \over 2\Delta x$ 식을 사용함

## 2. 편미분 (Partial Derivative)
* 예시)  
  * $f(x,y) = x^2 + 2xy + y^2$
  * ${\partial f(x,y) \over \partial x} = {\partial (x^2 + 2xy + y^2) \over \partial x} = 2x + 2y$

## 3. Chain Rule
* 공식
  * $F(x) = f(g(x))$
  * $F'(x)$ $\rightarrow$ $f'((g(x)) \cdot g'(x)$

## 4. 경사하강법(Gradient Descent)
* 경사하강법 (Gradient Descent, 이하 GD)는 위에서 거론 됐던 오차 함수인 𝜀 을 최소화 하는 𝑎,𝑏 를 찾을 수 있는 최적화 알고리즘 중의 하나임.
* 경사하강법은 임의의 a, b를 선택한 후 (random initialization)에 기울기 (gradient)를 계산해서 기울기 값이 낮아지는 방향으로 진행
* 계산법
  * $a_{n+1} = a_n - \eta ∇ f(a_n)$
  * $b_{n+1} = b_n - \eta ∇ f(b_n)$
  * 반복적으로 파라미터 a,b를 업데이트 해가면서 그래디언트( ∇f )가 0이 될 때까지 이동
  * 학습률 (learning rate,  η )
    * 학습률이 너무 낮게 되면 알고리즘이 수렴하기 위해서 반복을 많이 해야되고 이는 결국 수렴에 시간을 상당히 걸리게 합니다. 반대로 학습률이 너무 크면 오히려 극소값을 지나쳐 버려서 알고리즘이 수렴을 못하고 계산을 계속 반복하게 될 수 있다.


```python
import numpy as np
def gradient_descent(X, y, lr = 0.05, epoch = 10):
    
    a, b = 0.33, 0.48 # 임의 선택한 파라미터 a, b
    N = len(X) # 샘플 갯수
    
    for _ in range(epoch):            
        f = y - (a*X + b)
    
        # a와 b를 업데이트 합니다
        a -= lr * (-2 * X.dot(f).sum() / N)
        b -= lr * (-2 * f.sum() / N)        
        
    print('a: '+str(a))
    print('b: '+str(b))

# y = 3 x + 5
X = np.array([1, 2, 3, 4, 5])
y = np.array([8, 11, 14, 17, 20])

gradient_descent(X,y)  # 에포크: 10번만 돌렸을 때

# epoch(에포크)를 수정하면 하나의 값으로 수렴한다.

```

    a: 3.8200706153280004
    b: 2.039284272128

