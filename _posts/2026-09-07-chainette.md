---
layout: post
title: Problème de la chaînette
date: 2026-09-07
description: Quelle est la forme d'une corde supendu ?
tags: physics
categories:
related_posts: false
---

<!-- $$\newcommand{\R}{\mathbb{R}}$$ -->
<!-- Importing macros (no arguments !) -->

{% assign macros = site.data.latex_macros.macros %}

<div style="display: none">
$$
{% for macro in macros %}\newcommand{\{{ macro[0] }}}{ {{ macro[1] }} }
{% endfor %}
$$
</div>

$$\newcommand{\d}{\mathrm{d}}$$

Le problème de la chaînette consiste à trouver l'équation d'une corde suspendue entre deux points. C'est un agréable mélange de modélisation, et de manipulation mathématique. L'équation différentielle résultante est moins classique qu'une simple EDL2, rencontrée tant de fois en licence ou classe préparatoire. La forme de la courbe obtenue a toutefois une expression simple à l'aide de fonction usuelles. 

# Exercice : la chaînette 

Une corde sans raideur de masse $m$ et de longueur $l$ est accrochée à ses deux extrémités en deux points de même hauteur et situés en $x = -a/2$ et $x= a/2$.  Quelle est la forme de la courbe $h(x)$ décrite par la corde ?

# Résolution 1
*Référentiel :* Terrestre Galiléen.

*Coordonnées :* Cartésiennes $(O,\vec{e_x},\vec{e_z})$ ou O est le bas de la corde.

On applique le principe fondamental de la dynamique (PFD) à une longueur infinitésimale de corde entre $x$ et $x+dx$, assimilée, au premier ordre au segment $\overrightarrow{\d M} = (\d x, \dot h(x)\d x)$. 
*Masse :* On note $\gamma=\frac{m}{l}$ la densité linéique de la corde. Par Pythagore, $\d m = \gamma \| \overrightarrow{\d M} \|^2 = \gamma \sqrt{1 + \dot h(x)^2}\d x$.

*Bilan des forces:* Gravité $-\d m g \vec{e_z} = $. Tension de la section de droite $\vec T(x+dx)$. Tension de la section de gauche $-\vec T(x)$. Le PFD à l'équilibre donne

$$
\begin{equation}
    \vec T(x+dx) - \vec T(x) - \gamma \sqrt{1 + \dot h(x)^2}\d x \vec{e_z} = 0,
\end{equation}
$$

c'est à dire, 
$$
\begin{equation}
\label{eq:ED_PFD} 
\frac{\d \vec T}{\d x} = \gamma \sqrt{1 + \dot h(x)^2} \vec{e_z}. \end{equation}
$$

Par projection sur $\vec{e_x}$, on a $T_x= cst = T_0$. Par projection sur $\vec{e_z}$ on a 
$$\begin{equation} \dot T_z =  \gamma \sqrt{1 + \dot h(x)^2} \end{equation}$$
On a une equation mais 2 inconnues ; il nous manque donc une equation pour résoudre le problème.
Mais puisque la corde est sans raideur, cela signifie que la tension est le long de la corde, c'est à dire que $\frac{T_z}{T_0} = \frac{\d h}{\d x} = \dot h$.

On substitue $\dot h$ par cette dernière expression dans l'équation \eqref{eq:ED_PFD} et on obtient,
$$
\begin{equation}
    \dot T_z = \gamma g \sqrt{1+T_z^2/T_0^2}
\end{equation}
$$
 


