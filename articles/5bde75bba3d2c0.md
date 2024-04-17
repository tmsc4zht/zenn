---
title: "多変量正規分布の積率母関数"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学", "数理統計"]
published: false
---

[現代数理統計学](https://amzn.asia/d/2pclk02)の多変量正規分布の積率母関数を求める式変形についての仕組みがわからなかったので、行間を埋めた。

----

## 積率母関数の定義

$n$次元の確率ベクトルを$Y = (Y_1, \dots, Y_n)^\mathsf{T}$とするとき、その積率母関数は以下で定義される。ただし、$\theta = (\theta_1, \dots, \theta_n)^\mathsf{T}$とする。

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
\phi(\theta) = \mathrm{E}(e^{\transpose{\theta}Y})
$$

## 多変量正規分布の確率分布関数

多変量正規分布の確率分布関数は以下で定義される。

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
f(y) = \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp{\left[-\frac{1}{2} \transpose{(y-\mu)} \Sigma (y-\mu) \right]}
$$ 

ここで、

よって、多変量正規分布の積率母関数は

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
\phi(\theta) = \mathrm{E}(e^{\transpose{\theta}Y})
 = \overbrace{ \int\dots\int }^n \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp{\left[-\frac{1}{2} \transpose{(y-\mu)} \Sigma (y-\mu) \right]} dy_1 \dots dy_n
$$ 

ここで、$\mu=(\mu_1, \dots, \mu_n)^\mathsf{T}$は$Y$の平均ベクトル、$\Sigma$は分散共分散行列を表す。

## 多変量正規分布の積率母関数

多変量正規分布の積率母関数を定義に従って求める。

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
\gdef\nint#1{
     \overbrace{ \int\dots\int }^n #1 dy_1 \dots dy_n \\
}

\begin{aligned} 
    \phi(\theta) &= \mathrm{E}(e^{\transpose{\theta}Y}) \\
    &= \nint{ e^{\transpose{\theta}y} \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp{\left[-\frac{1}{2} \transpose{(y-\mu)} \Sigma (y-\mu) \right]} } \\
\end{aligned} 

$$

指数関数を指数法則に従ってまとめると

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
\gdef\nint#1{
     \overbrace{ \int\dots\int }^n #1 dy_1 \dots dy_n \\
}

\begin{aligned} 
    &= \nint{  \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp{\left[\transpose{\theta} y -\frac{1}{2} \transpose{(y-\mu)} \Sigma (y-\mu) \right]} } \\
\end{aligned} 
$$ 

## 指数関数の中身の計算

準備として以下を展開する。

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{aligned} 
    \qform{(y-\mu)}{\Sigma}{(y-\mu)} &=
    {(\t{y}-\t{\mu})}{\Sigma}{(y-\mu)} \\ &=
    \qform{y}{\Sigma}{y} - \qform{y}{\Sigma}{\mu} - \qform{\mu}{\Sigma}{y} + \qform{\mu}{\Sigma}{\mu} \\ &=
    \qform{y}{\Sigma}{y} - 2 \qform{\mu}{\Sigma}{y} + \qform{\mu}{\Sigma}{\mu} 
\end{aligned} 
$$

よって

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{aligned} 
    \t{\theta} y -\frac{1}{2} \t{(y-\mu)} \Sigma (y-\mu)  &=
    -\frac{1}{2} \left[
        \qform{y}{\Sigma}{y} - 2 \qform{\mu}{\Sigma}{y} -2\qform{\theta}{}{y} + \qform{\mu}{\Sigma}{\mu} 
      \right]
\end{aligned} 

$$

ここで括弧内を平方完成することを考える。

:::message

行列で考える前に普通の（？）平方完成について復習すると以下のようになる。

$$
y^2+ay+b = \left(y + \frac{a}{2} \right)^2 + b - \frac{a}{4}
$$

$y$が一次の項の係数を1/2倍したものが括弧の中に入ります。
調整のために、その2乗を引きます。

行列の平方完成でも同じことを考えます。

:::




