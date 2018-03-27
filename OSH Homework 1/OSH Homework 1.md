# OSH Homework 1
<div align="right"><strong>吴永基 PB16001676</strong></div>
## Problem 1
### Job set
| Name | Arrive Time | Time Required | Deadline | Difficulty | 
|:----------:|:------------:|:------------:|:------------:|:------------:|
|OSH, Lab| 2 days ago | 2 days | 10 days left | 3 |
|Write a VGG16 Network| 5 days ago | 3 days | 20 days left | 4 |
|Probability, Homework| today | 1 day | 6 days left | 2 |
|Read PRML| 10 days ago | 20 days | 100 days left | 3 |
|Differential Equations, Homework| yesterday | 2 days | 10 days left | 5 |
|CSAPP Malloc Lab, Report| today | 1 day | 20 days left | 1 |
### Schedulable?
$$
\begin{align}
U & = \sum_{i=1}^{n} \frac{T_{\mathrm{cost}}(i)}{T_{\mathrm{remains}}(i)} \\
& = \frac{2}{10}+\frac{3}{20}+\frac{1}{6}+\frac{20}{100}+\frac{2}{10}+\frac{1}{20}\\
& \approx 0.967
\end{align}
$$
we have $U \leq 1$ So the set of jobs is schedulable.
### Scheduler
**PRINCIPLE: Earliest deadline first**
1. Probability, Homework
2. OSH, Lab
3. Differential Equations, Homework
4. CSAPP Malloc Lab, Report
5. Write a VGG16 Network
6. Read PRML

## Problem 2
Code for Context Switch:

```assembly
;void swtch(struct context **old, struct context *new);
swtch:
  ;save old registers
  movq 8(%rsp), %rax  ;put old ptr into eax
  popq 0(%rax)        ;save old IP
  movq %rsp, 8(%rax)
  movq %rbx, 16(%rax)
  movq %rcx, 24(%rax)
  movq %rdx, 32(%rax)
  movq %rsi, 40(%rax)
  movq %rdi, 48(%rax)
  movq %rbp, 56(%rax)

  ;load new registers
  movq 8(%rsp), %rax
  movq 56(%rax), %rbp
  movq 48(%rax), %rdi
  movq 40(%rax), %rsi
  movq 32(%rax), %rdx
  movq 24(%rax), %rcx
  movq 16(%rax), %rbx
  movq 8(%rax), %rsp
  pushq 0(%rax)
  ret
```