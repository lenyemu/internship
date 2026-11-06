---
title: "[예시] 최소제곱법 (Least Squares)"
categories: [Notes, 선형대수]
tags: [linear-algebra, regression, numpy]
author: lenyemu
description: "정규방정식 유도, 정사영으로 보는 기하학적 의미, 구현할 때 주의할 점"
math: true
---

> 노트가 어떤 모습인지 보여주기 위한 **예시 글**입니다. 실제 노트를 쓰기 시작하면 지워도 됩니다.
{: .prompt-info }

## 한 줄 요약

> 해가 없는 연립방정식 $$ Ax = b $$ 에서, 오차의 제곱합 $$ \lVert Ax - b \rVert_2^2 $$ 을 가장 작게 만드는 $$ x $$ 를 찾는 방법.
{: .prompt-tip }

## 문제 설정

관측 데이터가 행렬 $$ A \in \mathbb{R}^{m \times n} $$ ($$ m > n $$), 관측값이 $$ b \in \mathbb{R}^{m} $$ 일 때,
식의 개수가 미지수보다 많으므로 보통 $$ Ax = b $$ 를 정확히 만족하는 해는 없습니다. 대신 다음을 풉니다.

$$
\hat{x} = \arg\min_{x \in \mathbb{R}^n} \lVert Ax - b \rVert_2^2
$$

## 정규방정식 유도

목적 함수를 전개하면

$$
f(x) = (Ax - b)^\top (Ax - b) = x^\top A^\top A x - 2\, b^\top A x + b^\top b
$$

이고, 기울기를 0으로 두면

$$
\nabla f(x) = 2 A^\top A x - 2 A^\top b = 0
$$

이므로 **정규방정식(normal equation)** 을 얻습니다.

$$
\begin{equation}
  A^\top A \, \hat{x} = A^\top b
  \label{eq:normal}
\end{equation}
$$

$$ A $$ 의 열들이 선형독립(full column rank)이면 $$ A^\top A $$ 는 가역이고, $$ \hat{x} = (A^\top A)^{-1} A^\top b $$ 입니다.

## 기하학적 의미

식 \eqref{eq:normal} 을 $$ A^\top (b - A\hat{x}) = 0 $$ 으로 고쳐 쓰면, **잔차 $$ r = b - A\hat{x} $$ 가 $$ A $$ 의 열공간에 수직**이라는 뜻입니다.
즉 $$ A\hat{x} $$ 는 $$ b $$ 를 $$ A $$ 의 열공간에 **정사영(projection)** 한 점이고, 정사영 행렬은 다음과 같습니다.

$$
P = A (A^\top A)^{-1} A^\top, \qquad A\hat{x} = Pb
$$

## 구현할 때 주의할 점

> $$ (A^\top A)^{-1} $$ 을 직접 계산하지 마세요. $$ A^\top A $$ 의 조건수는 $$ \kappa(A)^2 $$ 이라서 수치 오차가 크게 불어납니다.
> QR 분해나 SVD 기반의 `np.linalg.lstsq` 를 쓰는 것이 안전합니다.
{: .prompt-warning }

```python
import numpy as np

rng = np.random.default_rng(0)
m, n = 100, 3
A = rng.normal(size=(m, n))
x_true = np.array([1.0, -2.0, 0.5])
b = A @ x_true + 0.1 * rng.normal(size=m)

# 권장: SVD 기반 최소제곱
x_hat, *_ = np.linalg.lstsq(A, b, rcond=None)

# 비교용: 정규방정식 (작고 조건이 좋은 문제에서만)
x_normal = np.linalg.solve(A.T @ A, A.T @ b)

print(x_hat)                        # x_true 에 가까운 값
print(np.allclose(x_hat, x_normal)) # True
```
{: file="least_squares.py" }

## 참고 자료

- G. Strang, *Introduction to Linear Algebra*, 4.3절 Least Squares Approximations
- [NumPy `linalg.lstsq` 문서](https://numpy.org/doc/stable/reference/generated/numpy.linalg.lstsq.html)
