# smali基本语法


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

例子2
----------
```java
package com.example.nurmemet.smalltest;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        test();
    }




    private void test(){
        int a=0;
        System.out.println(a++);
        System.out.println(a);
    }
}





.class public Lcom/example/nurmemet/smalltest/MainActivity;
.super Landroid/support/v7/app/AppCompatActivity;
.source "MainActivity.java"


# direct methods
.method public constructor <init>()V
    .registers 1

    .prologue
    .line 6
    invoke-direct {p0}, Landroid/support/v7/app/AppCompatActivity;-><init>()V

    return-void
.end method

.method private test()V
    .registers 4

    .prologue
    .line 19
    const/4 v0, 0x0    #寄存器v0默认初始化为0

    .line 20
    .local v0, "a":I  #本地寄存器v0 ,类型int  ,别名a
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;  #java/lang/System 类 里面的 out变量 放到寄存器v2 中 #变量类型为 java/io/PrintStream

    add-int/lit8 v1, v0, 0x1   #v0加1 结果放到v1

    .end local v0    # "a":I  
    .local v1, "a":I
    invoke-virtual {v2, v0}, Ljava/io/PrintStream;->println(I)V

    .line 21
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;  #同上，把变量out放到寄存器v2中

    invoke-virtual {v2, v1}, Ljava/io/PrintStream;->println(I)V  #调用方法println 

    .line 22
    return-void
.end method


# virtual methods
.method protected onCreate(Landroid/os/Bundle;)V
    .registers 3
    .param p1, "savedInstanceState"    # Landroid/os/Bundle;

    .prologue
    .line 10
    invoke-super {p0, p1}, Landroid/support/v7/app/AppCompatActivity;->onCreate(Landroid/os/Bundle;)V

    .line 11
    const v0, 0x7f040019

    invoke-virtual {p0, v0}, Lcom/example/nurmemet/smalltest/MainActivity;->setContentView(I)V

    .line 12
    invoke-direct {p0}, Lcom/example/nurmemet/smalltest/MainActivity;->test()V   #invoke-direct 调用本类方法，注意跟 #invoke-virtual区分

    .line 13
    return-void
.end method



```

例子3
---------------
```java
package com.example.nurmemet.smalltest;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        test();
    }




    private void test(){

        for (int i=0;i<5;i++){
            Log.d("test",String.valueOf(i));
        }
    }
}




```

```smali
.class public Lcom/example/nurmemet/smalltest/MainActivity;
.super Landroid/support/v7/app/AppCompatActivity;
.source "MainActivity.java"


# direct methods
.method public constructor <init>()V
    .registers 1

    .prologue
    .line 7
    invoke-direct {p0}, Landroid/support/v7/app/AppCompatActivity;-><init>()V

    return-void
.end method

.method private test()V
    .registers 4

    .prologue
    .line 21
    const/4 v0, 0x0

    .local v0, "i":I
    :goto_1
    const/4 v1, 0x5

    if-ge v0, v1, :cond_10

    .line 22
    const-string v1, "test"

    invoke-static {v0}, Ljava/lang/String;->valueOf(I)Ljava/lang/String;

    move-result-object v2

    invoke-static {v1, v2}, Landroid/util/Log;->d(Ljava/lang/String;Ljava/lang/String;)I

    .line 21
    add-int/lit8 v0, v0, 0x1

    goto :goto_1

    .line 24
    :cond_10
    return-void
.end method


# virtual methods
.method protected onCreate(Landroid/os/Bundle;)V
    .registers 3
    .param p1, "savedInstanceState"    # Landroid/os/Bundle;

    .prologue
    .line 11
    invoke-super {p0, p1}, Landroid/support/v7/app/AppCompatActivity;->onCreate(Landroid/os/Bundle;)V

    .line 12
    const v0, 0x7f040019

    invoke-virtual {p0, v0}, Lcom/example/nurmemet/smalltest/MainActivity;->setContentView(I)V

    .line 13
    invoke-direct {p0}, Lcom/example/nurmemet/smalltest/MainActivity;->test()V

    .line 14
    return-void
.end method


````


