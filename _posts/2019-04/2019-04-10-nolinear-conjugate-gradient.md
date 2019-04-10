---
layout: post
title: "Nonlinear conjugate gradient"
subtitle: "A simple introduction"
author: Yi Zhang
date: 2019-04-10 14:00:00 -0800
category:  document
tags: [optimization]
header-img: "img/gravity-wave.jpg"
---

* content
{:toc}

## 非线性共轭梯度法-DY法

1. 算法可用于求解形如$min(f(x))$的非线性最优化问题，解的迭代形式为$x\_{k+1}=x\_k+a\_kd\_k$。其中$a\_k$为迭代步长，$d\_k$为迭代方向。（不同的$d\_k$计算方法即为不同的非线性共轭梯度算法，它们对于$a\_k$计算的要求也各有区别。）
2. 要求目标函数$f(x)$连续可微且梯度$g(x)$已知。
3. DY法具有全局收敛性，但有一定几率陷入局部极小值。
4. DY法具有二次终止性，迭代终止于零梯度值位置或者$f(x) \leq threshold$处。

### 算法描述

* step 1 -\> 给出解的初值$f(x\_0)$并计算其梯度$g(x\_0)$，如果$\left\lVert g(x\_0) \right\rVert = 0$则算法终止，说明$x\_0$是$f(x)$的全局或局部极小解。否则设置$d\_0 = -g\_0$作为初始迭代方向（即解的最速下降方向）。
* step 2 -\> 执行满足如下所示的标准Wolfe条件的非精确线性搜索，计算得到$a\_k$。
    $f(x\_k+a\_k d\_k)-f(x\_k) \leq c\_1 a\_k {g\_k}^T d\_k$，
    ${g(x\_k+a\_k d\_k)}^T d\_K \> c\_2 {g\_k}^T d\_k$
    其中$0\< c\_1 \< c\_2 \< 1$，一般取$c\_1=0.1$，$c\_2 \in (0.6,0.8)$。对于重磁非线形反演一般取$c\_1=1e-4$，$c\_2=0.9$。
* step 3 -\> 更新$x_{k+1}=x\_k+a\_kd\_k $，若$\left\lVert g(x_{k+1}) \right\rVert = 0 $则算法终止，说明$x\_{k+1}$是$f(x)$的全局或局部极小解。否则继续step 4。
* step 4 -\> 更新$d_{k+1}=-g_{k+1}+\beta\_k d\_k$，其中$\beta\_k = \left\lVert g_{k+1} \right\rVert / {d_k}^T (g_{k+1}-g\_k)$。$k:=k+1$返回step 2。

### C++代码

func.h
```cpp
    #ifndef _FUNC_H  
    #define _FUNC_H

    double func_f(double x[])
    {
        double f0,f1,f2;
        f0 = 3*x[0] + x[1] + 2*x[2]*x[2] - 3;
        f1 = -3*x[0] + 5*x[1]*x[1] + 2*x[0]*x[2] - 1;
        f2 = 25*x[0]*x[1] + 20*x[2] + 12;
        return sqrt(f0*f0+f1*f1+f2*f2);
    }
    
    void func_g(double x[], double g[])
    {
        double f0,f1,f2,temp;
        f0 = 3*x[0] + x[1] + 2*x[2]*x[2] - 3;
        f1 = -3*x[0] + 5*x[1]*x[1] + 2*x[0]*x[2] - 1;
        f2 = 25*x[0]*x[1] + 20*x[2] + 12;
        temp = 0.5/sqrt(f0*f0+f1*f1+f2*f2);
    
        g[0] = temp*(6*f0+2*f1*(2*x[2]-3)+50*f2*x[1]);
        g[1] = temp*(2*f0+20*f1*x[1]+50*f2*x[0]);
        g[2] = temp*(8*f0*x[2]+4*f1*x[0]+40*f2);
    }
    #endif
```

main.cpp
```cpp
    #include "iostream"  
    #include "fstream"  
    #include "string"  
    #include "cmath"  
    #include "stdio.h"  
    #include "stdlib.h"  
    #include "func.h"  
    
    using namespace std;
    
    class cgdy
    {
    public:
        cgdy();
        ~cgdy();
    
        void linearSearch_Wolfe(double);
        void cg();
    private:
        double x[3];
        double x_temp[3];
        double g[3];
        double g_temp[3];
        double dk[3];
        double beta;
        double ak;
    
        double c1, c2;
    };
    
    cgdy::cgdy()
    {
    
    }
    
    cgdy::~cgdy()
    {
        cout << "x0 = " << x[0] << endl
            << "x1 =  " << x[1] << endl
            << "x2 =  " << x[2] << endl;
    }
    
    void cgdy::linearSearch_Wolfe(double init_ak)
    {
        //搜索符合Wolfe条件的ak值，ak的初始值大于零
        //DY算法主要计算均在这一段
        ak = init_ak;
        double gTdk,g2Tdk,df;
        gTdk = g[0]*dk[0]+g[1]*dk[1]+g[2]*dk[2];
    
        x_temp[0] = x[0] + ak*dk[0];
        x_temp[1] = x[1] + ak*dk[1];
        x_temp[2] = x[2] + ak*dk[2];
    
        func_g(x_temp,g_temp);
        g2Tdk = g_temp[0]*dk[0]+g_temp[1]*dk[1]+g_temp[2]*dk[2];
        df = func_f(x_temp)-func_f(x);
    
        int count = 0;
        while(df > c1*ak*gTdk || g2Tdk <= c2*gTdk)
        {
            ak = 0.5*ak/(1-df/(ak*gTdk));
    
            x_temp[0] = x[0] + ak*dk[0];
            x_temp[1] = x[1] + ak*dk[1];
            x_temp[2] = x[2] + ak*dk[2];
    
            func_g(x_temp,g_temp);
            g2Tdk = g_temp[0]*dk[0]+g_temp[1]*dk[1]+g_temp[2]*dk[2];
            df = func_f(x_temp)-func_f(x);
    
            if (fabs(ak)<=1e-30)
            {
                cout << "current ak is too small, break out"<<endl;
                break;
            }
        }
    
        cout << "ak = " << ak << endl;
    }
    
    void cgdy::cg()
    {
        c1 = 1e-4;
        c2 = 0.9;
        x[0] = 0; x[1] = 0; x[2] = 0;
    
        func_g(x,g);
        dk[0] = -1*g[0]; dk[1] = -1*g[1]; dk[2] = -1*g[2];
    
        if((g[0]*g[0]+g[1]*g[1]+g[2]*g[2]) < 1e-30)
        {
            cout << "A local/global minimum is reached "<< endl;
            return;
        }
    
        int times = 0;
        while(func_f(x)>1e-7&&times<300)
        {
            cout << "iterator: " << times << " ,f(x) = " << func_f(x) << endl;
            linearSearch_Wolfe(1);
            x[0] += ak*dk[0];
            x[1] += ak*dk[1];
            x[2] += ak*dk[2];
    
            func_g(x,g_temp);
            if((g_temp[0]*g_temp[0]+g_temp[1]*g_temp[1]+g_temp[2]*g_temp[2]) < 1e-30)
            {
                cout << "A local/global minimum is reached "<< endl;
                return;
            }
            else
            {
                beta = (g_temp[0]*g_temp[0]+g_temp[1]*g_temp[1]+g_temp[2]*g_temp[2])/
                    (dk[0]*(g_temp[0]-g[0])+dk[1]*(g_temp[1]-g[1])+dk[2]*(g_temp[2]-g[2]));
    
                dk[0] = -1*g_temp[0] + beta*dk[0];
                dk[1] = -1*g_temp[1] + beta*dk[1];
                dk[2] = -1*g_temp[2] + beta*dk[2];
    
                g[0] = g_temp[0];
                g[1] = g_temp[1];
                g[2] = g_temp[2];
            }
    
            times++;
        }
    
        cout << "f0 = " << 3*x[0] + x[1] + 2*x[2]*x[2] - 3 << endl;
        cout << "f1 = " << -3*x[0] + 5*x[1]*x[1] + 2*x[0]*x[2] - 1 << endl;
        cout << "f2 = " << 25*x[0]*x[1] + 20*x[2]+12 << endl;
    }
    
    int main(int argc, char const *argv[])
    {
        cgdy c1;
        c1.cg();
        return 0;
    }
```