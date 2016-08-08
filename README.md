# csharp-interview
This repo contains questions used in my C# interviews. Some of them are problems from my daily work.
## When we should not use double?

Most of the time we use double or float when we need a non-integer number. However, sometimes using double or float can go wrong.
Consider this example from "effective java", I have 1 dollar, there are candies for 10cent, 20cent, 30cent and so on.
You buy one of each candy till you cannot afford it. How many candies do you buy? How many change do you get?
```csharp
var funds = 1.00;
var itemsBought = 0;
for (var price = 0.1; funds >= price; price += 0.1)
{
    funds -= price;
    itemsBought++;
}
Console.WriteLine(itemsBought); // 3
``` 
The output shows you can only buy 3. However, we know we can buy 4: 0.1$,
0.2$, 0.3$ and 0.4$. This is because double/float cannot exactly represent values like 0.1, 0.01, 
and it turns out that you have 0.39999999999999991 left, 
but you cannot afford a 40-cent-candy.

The correct way to do it is to use decimal
```csharp
var funds = 1.00m; //funds and price are decimal
var itemsBought = 0;
for (var price = .1m; funds >= price; price += .1m)
{
    funds -= price;
    itemsBought++;
}
Console.WriteLine(itemsBought);
```
## Sorting problem ##
Q: Design a method to sort an array of integers

A: Aha, an easy one, use bubble sort.

Q: What if you need to support sorting an array of doubles and floats

A: Use generics

Q: What if you need to support sorting an array of any objects

A: Um, object implements IComparable

```csharp
public void sort<T>(T[] array) where T:IComparable
{
    if (array == null || array.Length < 1) return;
    var ordered = false;
    for (var i = 0; i < array.Length-1 && !ordered; i++)
    {
        ordered = true;
        for (var j = 0; j < array.Length - i - 1; j++)
        {
            if (array[j].CompareTo(array[j+1]) > 0)
            {
                ordered = false;
                var temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
        }
    }
}
```
## When do you use reflection?

Normally, interface is preferred than reflection.
Using reflection, you lose the compile-time type checking, have 
verbose coding statement and performance suffers.

In some situations, reflection is inevitable, like remote procedure call,
class browser, code analysis tool, registration service, etc.

## The difference between Func, Action and Predicate. Can Predicate be replaced? Why we need Func and Action? Can Action be replaced?
