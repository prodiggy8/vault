Gradient Descent

Given $\hat{y}=\sigma(w^Tx + b)=\sigma(z)=\frac{1}{1+e^{-z}}$
$$J=\frac{1}{m}\sum_{i=1}^{m}\ell(\hat{y}^{(i)}, y^{(i)})$$
Want to find $w,b$ that minimize $J(w,b)$

Repeat:
$$w:=w-\alpha \; \frac{\partial J(w,b)}{\partial w}$$
$$b:=b-\alpha \; \frac{\partial J(w,b)}{\partial b}$$
