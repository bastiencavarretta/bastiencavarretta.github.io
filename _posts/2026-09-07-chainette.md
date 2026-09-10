---
layout: post
title: Problème de la chaînette
date: 2026-09-07
description: Quelle est la forme d'une corde supendu ?
tags: physics
categories:
related_posts: false
hidden: true
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

# Résolution 1 : Principe fondamental de la dynamique
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
\frac{\d \vec T}{\d x} = \gamma \sqrt{1 + \dot h(x)^2} \vec{e_z}. \end{equation}
$$

Par projection sur $\vec{e_x}$, on a $T_x= cst = T_0$. Par projection sur $\vec{e_z}$ on a 
$$\begin{equation}\label{eq:ED_PFD} \dot T_z =  \gamma \sqrt{1 + \dot h(x)^2} \end{equation}$$
On a une equation mais 2 inconnues ; il nous manque donc une equation pour résoudre le problème.
Mais puisque la corde est sans raideur, cela signifie que la tension est le long de la corde, c'est à dire que $\frac{T_z}{T_0} = \frac{\d h}{\d x} = \dot h$.

On substitue $\dot h$ par cette dernière expression dans l'équation \eqref{eq:ED_PFD} et on obtient,
$$
\begin{equation}
    \dot T_z = \gamma g \sqrt{1+T_z^2/T_0^2}
\end{equation}
$$

Pour résoudre cette équation, rien de plus naturel que de procéder par séparation des variables.
$$
\begin{equation}
    \frac{\d T_z}{\sqrt{1+T_z^2/T_0^2}} = \gamma g \d x
\end{equation}
$$
On intègre ces tranches infinitésimales entre $T(0)=0$ et $T(x)$ (resp. $0$ et $x$). Le terme de droite donne $\gamma g x$. Pour le terme de gauche, on effectue le changement de variable $T_z = T_0 \sinh(u)$, $\d T_z = T_0 \cosh(u) \d u$, et on utilise $1+\sinh^2 = \cosh^2$.

$$
\begin{equation}
\int_0^{T_z(x)} \frac{\d T_z}{\sqrt{1+T_z^2/T_0^2}} 
= \int_{\sinh^{-1}(0)}^{\sinh^{-1}(T_z(x)/T_0)} \frac{T_0 \cosh(u)}{\cosh(u)} \d u = T_0 \sinh^{-1}(T_z(x)/T_0)
\end{equation}
$$
En isolant $T_z(x)$ dans l'équation $T_0 \sinh^{-1}(T_z(x)/T_0) = \gamma g x$, on obtient, 
$T_z(x) = T_0 \sinh(\gamma g x/T_0)$. Il nous reste à primitiver cette fonction pour obtenir
$$
\begin{equation}
h(x) = \frac{T_0}{\gamma g} (\cosh(\gamma g x/T_0)-1)
\end{equation}
$$
où l'on a utilisé les conditions aux limites $h(0) = \dot h(0) = 0$, $x=0$ étant sur l'axe de symétrie du problème.


Pour rassurer les plus matheuses d'entre nous, deux choses peuvent jusitifier la séparation des variables:
1. Niveau Licence. En toute rigueur, cette étape est un changement de variable $w = T_z(x)$, $\d w = \dot  T_z(x) \d x$, où $T_z$ est inconnu (mais bijective car de dérivée positive).
2. Niveau Master. Les formes différentielles formalisent le $\d x$ d'une intégrale, et permettent de manipuler ces "tranches infinitésimales" sans perte de rigueur.

# Résolution 2 : Principe de moindre action
L'optimisateur préfère voir ce problème en terme d'action. Le système minimise son action $E_p - E_c$, et donc, à l'équilibre, son énergie potentielle. Par calcul des variation, la courbe $h$ doit vérifier l'équation d'Euler-Lagrange, $$\frac{\partial \mathcal{L}}{{\partial h}} - \frac{\d}{\d t} \left ( \frac{\partial \mathcal{L}}{{\partial \dot h}}\right ) = 0 $$
où $\mathcal{L}(h,\dot h) = \gamma \sqrt{1 + \dot h(x)^2} g h$ est en effet l'énergie potentielle du système. Ceci nous donne $ \sqrt{1 + \dot h(x)^2} - \frac{\d}{\d t} h \frac{\ddot h}{\sqrt{1 + \dot h(x)^2}}= 0$, i.e. 