# csharp-interview
This repo contains questions used in my C# interviews. Some of them are problems from my daily work.
## When to use decimal?

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
This is because double/float cannot exactly represent values like 0.1, 0.01, you have 0.39999999999999991 left, 
but you cannot afford a 40-cent-candy.

The correct way to do it is to use decimal
```csharp
var funds = 1.00m;
var itemsBought = 0;
for (var price = .1m; funds >= price; price += .1m)
{
    funds -= price;
    itemsBought++;
}
Console.WriteLine(itemsBought);
```