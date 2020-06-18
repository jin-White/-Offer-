# -Offer-
以标签分类
数学：
1.面试题44
数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

class Solution {
public:
    int findNthDigit(int n) {
        long base = 9,digit = 1;
        while(n - base*digit> 0){
            n -= base*digit;
            base *=10;
            digit++;
        }

        int idx = n % digit;  // 注意由于上面的计算，n现在表示digits位数的第n个数字
        if (idx == 0)idx = digit;
        long num = 1;
        for (int i = 1;i < digit;i++)
            num *= 10;
        num += (idx == digit)? n/digit - 1:n/digit;

        for (int i=idx;i<digit;i++) num /= 10;
        return num % 10;
    }
};

class Solution {
public:
    int findNthDigit(int n) {
        n -= 1;
        for (long digits=1;digits < 11;++digits ){
            int first_num = pow(10,digits-1);
            if (n < 9 * first_num * digits){
                return int(to_string(first_num + n/digits)[n%digits])-'0';
            }
            n -= 9 * first_num * digits;
        }
        return 0;
    }
};
