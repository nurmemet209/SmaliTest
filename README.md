# SmaliTest


```java
package com.example.nurmemet.smalltest;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}


/*smali 代码*/
/*
//完整的类名称
.class public Lcom/example/nurmemet/smalltest/MainActivity;
.super Landroid/support/v7/app/AppCompatActivity;
.source "MainActivity.java"  //源文件

//构造方法
# direct methods
.method public constructor <init>()V
    .registers 1

    .prologue
    .line 6
    invoke-direct {p0}, Landroid/support/v7/app/AppCompatActivity;-><init>()V

    return-void
.end method


# virtual methods
.method protected onCreate(Landroid/os/Bundle;)V
    .registers 3        //本方法需要三个寄存器，两个参数寄存器，一个非参数寄存器
    .param p1, "savedInstanceState"    # Landroid/os/Bundle;

    .prologue     //方法开始
    .line 10
    invoke-super {p0, p1}, Landroid/support/v7/app/AppCompatActivity;->onCreate(Landroid/os/Bundle;)V
    //p0 相当于this  每个非静态方法的第一个参数必须是this  注意命名规则 p是命名参数寄存器的
    .line 11
    const v0, 0x7f040019   //0x7f040019赋值给v0寄存器
    //invoke-virtual 调用超类的方法
    invoke-virtual {p0, v0}, Lcom/example/nurmemet/smalltest/MainActivity;->setContentView(I)V    //V 是返回值， 表示 void

    .line 12
    return-void
.end method



//下面是函数返回值的表示方法
V  void，只能用于返回值类型
Z  boolean
B  byte
S  short
C  char
I  int
J  long（64位）
F  float
D  double(64位)
*/

```

