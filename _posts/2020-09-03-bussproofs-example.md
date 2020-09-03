---
layout: post
date: 2020-09-03 KST
author: Sori Lee
---

# Bussproofs Example

Here is an example proof tree drawn with `bussproofs`:

\begin{prooftree}
      \AxiomC{}
      \RightLabel{Hyp$^{1}$}
      \UnaryInfC{$P$}
            \AXC{$P\to Q$} % short for \AxiomC
      \RL{$\to_E$} % short for \RightLabel
      \BinaryInfC{$Q^2$}
                  \AXC{$Q\to R$}
      \RL{$\to_E$}
      \BIC{$R$} % short for \BinaryInfC
                        \AXC{$Q$}
                        \RL{Rit$^2$}
                        \UIC{$Q$} % short for \UnaryInfC
      \RL{$\wedge_I$}
      \BIC{$Q\wedge R$}
      \RL{$\to_I$$^1$}
      \UIC{$P\to Q\wedge R$}
\end{prooftree}
