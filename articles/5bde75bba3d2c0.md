---
title: "多変量正規分布の積率母関数"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学", "数理統計"]
published: true
---

[現代数理統計学](https://amzn.asia/d/2pclk02)の多変量正規分布の積率母関数を求める式変形についての仕組みがわからなかったので、行間を埋めた。

----

## 積率母関数の定義

$n$次元の確率ベクトルを$Y = (Y_1, \dots, Y_n)^\mathsf{T}$とするとき、その積率母関数は以下で定義される。ただし、$\theta = (\theta_1, \dots, \theta_n)^\mathsf{T}$とする。

$$
\gdef\transpose#1{#1^{\mathsf{T}}}
\phi(\theta) = \mathrm{E}(e^{\transpose{\theta}Y})
$$

## 多変量正規分布の確率密度関数

多変量正規分布の確率密度関数は以下で定義される。

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}
f(y) = \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
       \exp{\left[
          -\frac{1}{2} \qform{(y-\mu)}{\Sigma^{-1}}{(y-\mu)}
         \right]}
$$ 

ここで、$\mu=(\mu_1, \dots, \mu_n)^\mathsf{T}$は$Y$の平均ベクトル、$\Sigma$は分散共分散行列を表す。
また、この分布を$\mathrm{N}_n(\mu, \Sigma)$と表す。

## 多変量正規分布の積率母関数

多変量正規分布の積率母関数を定義に従って求める。

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\nint#1{
     \overbrace{ \int\dots\int }^n #1 dy_1 \cdots dy_n
}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*} 
    \phi(\theta) &= \mathrm{E}(e^{\t{\theta}Y}) \\
                 &= \nint{ e^{\t{\theta}y} \cdot \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
     \exp{\left[
        -\frac{1}{2} \qform{(y-\mu)}{\Sigma^{-1}}{(y-\mu)}
         \right]} }
\end{align*} 
$$

指数関数を指数法則に従ってまとめると

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\nint#1{
     \overbrace{ \int\dots\int }^n #1 dy_1 \cdots dy_n
}
\gdef\qform#1#2#3{\t{#1}#2#3}

= \nint{
      \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
       \exp{\left[
          \t{\theta} y -\frac{1}{2} \qform{(y-\mu)}{\Sigma^{-1}}{(y-\mu)}
       \right]}
   } 
$$ 

### 指数関数の中身の計算

準備として以下を展開する。

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*} 
    \qform{(y-\mu)}{\Sigma^{-1}}{(y-\mu)} &=
    {(\t{y}-\t{\mu})}{\Sigma^{-1}}{(y-\mu)} \\ &=
    \qform{y}{\Sigma^{-1}}{y} - \qform{y}{\Sigma^{-1}}{\mu} - \qform{\mu}{\Sigma^{-1}}{y} + \qform{\mu}{\Sigma^{-1}}{\mu} \\ &=
    \qform{y}{\Sigma^{-1}}{y} - 2 \qform{\mu}{\Sigma^{-1}}{y} + \qform{\mu}{\Sigma^{-1}}{\mu} 
\end{align*} 
$$

よって

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*} 
    \t{\theta} y -\frac{1}{2} \t{(y-\mu)} \Sigma^{-1} (y-\mu)  &=
    -\frac{1}{2} \left[
        \qform{y}{\Sigma^{-1}}{y} - 2 \qform{\mu}{\Sigma^{-1}}{y} -2\qform{\theta}{}{y} + \qform{\mu}{\Sigma^{-1}}{\mu} 
      \right]
\end{align*} 

$$

ここで括弧内を平方完成することを考える。

:::message

行列で考える前に普通の（？）平方完成について復習する。

$y^2+ay+b$の平方完成において、目指す形は以下のようになる。

$$
y^2+ay+b = \left(y + \bigcirc \right)^2 + \square
$$

ここで、左辺を展開すると、

$$
y^2 + 2\bigcirc{}y + \bigcirc^2 + \square
$$


係数を比較することで以下の式が成り立つ

$$
\begin{align*}
a &= 2\bigcirc{} \\
b &= \bigcirc{}^2 + \square
\end{align*} 
$$

これを解くと

$$
\begin{align*}
\bigcirc{} &= \frac{a}{2} \\
\square &= -\frac{a^2}{4} + b
\end{align*} 
$$


行列の平方完成でも同じことを考える。

:::

平方完成の準備のために$y$の項をまとめる。


$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*}
 & \qform{y}{\Sigma^{-1}}{y} - 2 \qform{\mu}{\Sigma^{-1}}{y}  - 2\qform{\theta}{}{y}    + \qform{\mu}{\Sigma^{-1}}{\mu} \\
=& \qform{y}{\Sigma^{-1}}{y} + 2(- \qform{\mu}{\Sigma^{-1}}{} -  \qform{\theta}{}{})y  + \qform{\mu}{\Sigma^{-1}}{\mu} \\
\end{align*} 

$$

平方完成で目指す形は以下のようになる。(1)

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

 \qform{y}{\Sigma^{-1}}{y} + 2(- \qform{\mu}{\Sigma^{-1}}{} -  \qform{\theta}{}{})y  + \qform{\mu}{\Sigma^{-1}}{\mu} 
= \qform{\left(y + \bigcirc \right)}{\Sigma^{-1}}{\left(y + \bigcirc \right)} + \square 

$$

ここで、右辺を展開すると、

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}


\begin{align*}
& \qform{\left(y - \bigcirc \right)}{\Sigma^{-1}}{\left(y - \bigcirc \right)} + \square  \\
=& \qform{y}{\Sigma^{-1}}{y} + \qform{\bigcirc}{\Sigma^{-1}}{y} + \qform{y}{\Sigma^{-1}}{\bigcirc} + \qform{\bigcirc}{\Sigma^{-1}}{\bigcirc} + \square \\
=& \qform{y}{\Sigma^{-1}}{y} + 2 \qform{\bigcirc}{\Sigma^{-1}}{y} + \qform{\bigcirc}{\Sigma^{-1}}{\bigcirc} + \square \\
\end{align*} 

$$

となる。

よって(1)の$y$の1次の係数を比較すると

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}


\begin{align*}
2\qform{\bigcirc}{\Sigma^{-1}}{} &=  2(-\qform{\mu}{\Sigma^{-1}}{} - \qform{\theta}{}{}) \\
 \qform{\bigcirc}{}{}            &= -\qform{\mu}{}{} - \qform{\theta}{\Sigma}{} \\
 \bigcirc            &= -\mu - {\Sigma}{\theta} \\
\end{align*} 

$$

$y$の0次の項を比較すると、

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}
\gdef\msm{\qform{\mu}{\Sigma^{-1}}{\mu}}

\begin{align*}
    \square + \qform{\bigcirc}{\Sigma^{-1}}{\bigcirc} &= \msm \\
    \square &= - \qform{\bigcirc}{\Sigma^{-1}}{\bigcirc}                          &+ \msm \\
    \square &= - \qform{(-\mu -\Sigma\theta)}{\Sigma^{-1}}{(-\mu - \Sigma\theta)} &+ \msm \\
    \square &= - \qform{(-\mu -\Sigma\theta)}{}{(-\Sigma^{-1}\mu - \theta)}       &+ \msm \\
    \square &= - (-\t{\mu} -\t{\theta}\Sigma){(-\Sigma^{-1}\mu - \theta)}         &+ \msm \\
    \square &= - (+\t{\mu} +\t{\theta}\Sigma){(+\Sigma^{-1}\mu + \theta)}         &+ \msm \\
    \square &= - (\msm + \qform{\mu}{}{\theta} + \qform{\theta}{}{\mu} + \qform{\theta}{\Sigma}{\theta} )        &+ \msm \\
    \square &= - \qform{\mu}{}{\theta} - \qform{\theta}{}{\mu} - \qform{\theta}{\Sigma}{\theta}  \\
    \square &= -2 \qform{\theta}{}{\mu} - \qform{\theta}{\Sigma}{\theta}  
\end{align*} 

$$

以上をまとめると、

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*}
 & \qform{y}{\Sigma^{-1}}{y} - 2 \qform{\mu}{\Sigma^{-1}}{y}  - 2\qform{\theta}{}{y}    + \qform{\mu}{\Sigma^{-1}}{\mu} \\
=& \qform{\left(y - (\mu + \Sigma\theta) \right)}{\Sigma^{-1}}{\left(y - (\mu +\Sigma\theta) \right)} -2 \qform{\theta}{}{\mu} - \qform{\theta}{\Sigma}{\theta} 
\end{align*} 

$$

以上の結果より、指数関数の中身を改めて計算すると、

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*} 
    & \t{\theta} y -\frac{1}{2} \t{(y-\mu)} \Sigma^{-1} (y-\mu)  \\
     =& -\frac{1}{2} \left[
        \qform{y}{\Sigma^{-1}}{y} - 2 \qform{\mu}{\Sigma^{-1}}{y} -2\qform{\theta}{}{y} + \qform{\mu}{\Sigma^{-1}}{\mu} 
      \right] \\
     =& -\frac{1}{2} \left[
 \qform{\left(y - (\mu + \Sigma\theta) \right)}{\Sigma^{-1}}{\left(y - (\mu +\Sigma\theta) \right)} -2 \qform{\theta}{}{\mu} - \qform{\theta}{\Sigma}{\theta} 
      \right] \\
     =& -\frac{1}{2} \left[
        \qform{\left(y - (\mu + \Sigma\theta) \right)}{\Sigma^{-1}}{\left(y - (\mu +\Sigma\theta) \right)}
        \right] + \qform{\theta}{}{\mu} + \frac{\qform{\theta}{\Sigma}{\theta}}{2}
      
\end{align*} 
$$

となる。

### 積分に戻る

以上の計算をもとの積分に代入する。

$$
\gdef\nint#1{
     \overbrace{ \int\dots\int }^n #1 dy_1 \cdots dy_n
}
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\begin{align*} 
\phi(\theta) = & \nint{
      \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
       \exp{\left[
          \t{\theta} y -\frac{1}{2} \qform{(y-\mu)}{\Sigma^{-1}}{(y-\mu)}
       \right]}
   }  \\
  =& \nint{
      \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
       \exp{\left[

      -\frac{1}{2} \left[
        \qform{\left(y - (\mu + \Sigma\theta) \right)}{\Sigma^{-1}}{\left(y - (\mu +\Sigma\theta) \right)}
        \right] + \qform{\theta}{}{\mu} + \frac{\qform{\theta}{\Sigma}{\theta}}{2}

       \right]}
   }  \\
  =& \nint{
      \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}}
       \exp{\left[

      -\frac{1}{2} \left[
        \qform{\left(y - (\mu + \Sigma\theta) \right)}{\Sigma^{-1}}{\left(y - (\mu +\Sigma\theta) \right)}
        \right] 

       \right]}
   }  \cdot \exp{\left(
    \qform{\theta}{}{\mu} + \frac{\qform{\theta}{\Sigma}{\theta}}{2} 
   \right)
   } 


\end{align*} 
$$ 

ここで、積分される関数の形をよく見ると、多変正規分布の確率密度関数と同じ形をしている。
具体的には、$\mathrm{N}_n(\mu + \Sigma\theta, \Sigma)$の確率密度関数とみなせる。
分布関数を全域で積分すると1になるので、多次元正規分布の積率母関数は、

$$
\gdef\t#1{#1^{\mathsf{T}}}
\gdef\qform#1#2#3{\t{#1}#2#3}

\phi(\theta) = \exp{\left(
    \qform{\theta}{}{\mu} + \frac{\qform{\theta}{\Sigma}{\theta}}{2} 
   \right)}

$$

となる。

行列の性質をもっとうまく使えば簡単になる気がする…