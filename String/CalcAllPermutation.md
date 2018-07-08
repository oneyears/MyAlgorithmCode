### 输入字符串，获得其所有的排序方式

- #### 递归实现

 1. 先从一个循环来确定第一个值a
 2. 再从第一个值里获得剩下两个交换值abc acb
 3. 然后返回成abc 交换获得第二个值b
 4. 然后再以b获得剩下两个排序 bac bca
 5. 然后继续返回成 abc 交换第三个值c
 6. 然后再以c获得剩下两个排序 cba cab
 7. 这里的循环里写了两个交换，其实就是交换其值让其作为首步
 ==然后回来交换回abc== 接着第一个和第三个进行交换
 
```
		public static void CalcAllPermutation_1(char [] perm,int _from,int _to) {
			if (_to <= 1) {
				return;
			} 
			if (_to == _from) {
				Console.WriteLine (perm);
			}

			for (int j = _from; j < _to; j++) {
				Swap<char> (ref perm [j],ref perm [_from]);
				CalcAllPermutation_1 (perm, _from+1, _to);
				Swap<char>(ref perm[j],ref perm[_from]);
			}
		}
		
		public static void Swap_1<T>(ref T lhs, ref T rhs) {
			T temp = lhs;
			lhs = rhs;
			rhs = temp;
		}

```

- #### 字典序排列
1. 从后往前找一个值（该值小于后面的值），（即该值比后面的值小则找到）取其下标为i
2. 从后找比上步骤大的值，找到后取其下标
3. 交换i，j两个对应的下标的值
4. 从i+1 到尾部全部反转，得到需要的值
5. 时间复杂度为o(n!)




```		
        public static void Main(){
			string str = "12345";
			char[] _charGroup = str.ToCharArray ();
			char[] _endGroup = { '5', '4', '3', '2', '1'};
			while(_charGroup != _endGroup)
			if (CalcAllPermutation2 (ref _charGroup, 5)) {
				Console.WriteLine (_charGroup);
			}
		}
		
		//得到这个字符串的下一个排序
		public static bool CalcAllPermutation_2(ref char [] perm,int _permLength) {
			int i;
			for (i = _permLength - 2; (i >= 0) && perm [i] >= perm [i + 1]; i--)
				;
			if (i < 0) {
				return false;
			}
			int j;
			for (j = _permLength - 1;( j > 1) && (perm [j] <= perm [i]); j--)
				;

			Swap_1<char> (ref perm [i], ref perm [j]);
			i ++;
			//长度本身加了1 直接减去下标i就是剩下的个数了
			Array.Reverse (perm, i, _permLength-i);
		
			return true;
		}
```