--------------------------------------------------------------------------------------------------------

     打印出杨辉三角，可以根据它其中的一条性质来作为思想的入口：第i行的第j个数等于第i-1行的第j-1位加上第j位数，
     
     即a[i][j]=a[i-1][j-1]+a[i-1][j]。

--------------------------------------------------------------------------------------------------------



```c


          # include <stdio.h>
          # include <string.h>
          
          int main()
          {
               int arr[10][10]={{1}};
               int line, row,space;
          
               for (line = 0; line < 10; line++)
               {
                    for (row = 0; row <=line; row++)
                    {
                         if (line < 2)                            //前两行为1
                         {
                              arr[line][row] = arr[0][0];
                         }
                         else if (row == 0 || row == line)        //首尾元素为1
                         {
                              arr[line][row] = arr[0][0];
                         }
                         else                                     //利用性质赋值
                         {
                              arr[line][row] = (arr[line - 1][row - 1] + arr[line - 1][row]);
                         }
                    }
               }
               
               for (line = 0; line < 10; line++)              //输出
               {
                    for (row = 0; row <= line; row++)
                    {
                         printf("%3d ", arr[line][row]);
                    }
                    
                printf("\n");
           }
          
               return 0;
          }


```



