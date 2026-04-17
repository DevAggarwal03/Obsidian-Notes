#### 1. groupby

- type 1
```python
df.groupby('country')['gdpPercap'].mean()
```
![[Pasted image 20260403125730.png]]

- type 2
```python
df.groupby(['continent', 'country'])[['lifeExp', 'gdpPercap']]
```
![[Pasted image 20260403125945.png]]


