2038. Remove colored pieces if both neighbors are the same color:
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        a = 0
        b = 0
        for i in range(1,len(colors)-1):
            if colors[i-1]==colors[i]==colors[i+1]:
                if colors[i] == 'A':
                    a += 1
                else:
                    b += 1
            
        return a-b>=1
```
with zip:
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        a,b=0,0
        for i,ii,iii in zip(colors,colors[1:],colors[2:]):
            if 'A'==i==ii==iii:a+=1
            elif 'B'==i==ii==iii:b+=1
        return b<a
```
