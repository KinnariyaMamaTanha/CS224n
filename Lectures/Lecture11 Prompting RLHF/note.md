# Prompting RLHF

log-devirative trick:

$$
\begin{align*}
    \nabla_\theta E_{s \sim p_\theta(s)}[f(s)] &= \nabla_{\theta}\sum_{s}^{}f(s)p_\theta(s) \\
    &=\sum_{s}^{}f(s)\nabla _\theta p_\theta(s) \\
    &=\sum_{s}^{}f(s)p_{\theta}(s)\nabla_\theta \log p_\theta(s) \\
    &=E_{s \sim p_\theta(s)}\left[f(s)\nabla_\theta \log_{} p_\theta (s) \right]
\end{align*} 
$$