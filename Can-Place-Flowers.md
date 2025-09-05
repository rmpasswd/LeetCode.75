### 605. Can Place Flowers

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.
Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule and false otherwise.  

Example 1:
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true  

Example 2:
Input: flowerbed = [1,0,0,0,1], n = 2
Output: false


**Solution:**
```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    // One approach could be this, did not try: search for this "000" substring in given input "10001"    // Index("000",str)

    // edge case [0 0]
    if len(flowerbed) ==2 && flowerbed[0] == 0 && flowerbed[1] == 0 && n <= 1{
        return true
    }
    // edge case [0]
    if len(flowerbed) ==1 && flowerbed[0] == 0 && n <= 1{
        return true
    }
    var NumN int= 0;

    // for i,value := range flowerbed {
    for  i:=0; i<len(flowerbed)-1; i++ {
        if i==0 {
            if flowerbed[i]==0 && flowerbed[i+1] == 0 {    // [0 0 ,.....]
                flowerbed[i]=1; 
                NumN+=1;
            } 
            continue; 
        } 

        if flowerbed[i] == 0 && flowerbed[i-1] ==0 && flowerbed[i+1] ==0 {   // [... 0 0 0 ... ]
            flowerbed[i]=1;
            NumN+=1;
        }
    }

    // edge case: [ ... 1 0 0 ]. Not [1 0 0 0]
    if flowerbed[len(flowerbed)-1] == 0 && flowerbed[len(flowerbed)-2] ==0 && flowerbed[len(flowerbed)-3] ==1 {
            NumN+=1;
    }

    if NumN>=n { return true;}
    return false;
}
```
<img width="1888" height="997" alt="image" src="https://github.com/user-attachments/assets/261f1f2a-f833-4038-a22c-145c4b39fe02" />  

Previous Approach, did not satisfy all cases!  
```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    // search for this "000" substring in given input "10001"
    // Index("000",str)

    var thriceCount, NumOfthrice int= 0,0;

    for _,value := range flowerbed {
        if value == 0 {thriceCount+=1;}
        if value == 1 {thriceCount = 0;}
        if thriceCount ==3 {
            thriceCount =1;
            NumOfthrice ++
        }
    }
    if thriceCount == 2 { // edge case: [1,0,0,0,0]

        NumOfthrice+=1;
    }
    if len(flowerbed)>2 {
        //edge case   // [0 0 1,0,....] 
        if flowerbed[0]==0 && flowerbed[1]==0 && flowerbed[2]==1{ 
            NumOfthrice+=1;
        }
        //edge case:      // [...,1,0,1,0,0]
        if flowerbed[len(flowerbed)-1]==0 && flowerbed[len(flowerbed)-2]==0 && flowerbed[len(flowerbed)-3]==1 { 
            NumOfthrice+=1;
        }
    }
    // edge case [0 0]
    if len(flowerbed) ==2 && flowerbed[0] == 0 && flowerbed[1] == 0 && n == 1{
        return true
    }
    // edge case [0]
    if len(flowerbed) ==1 && flowerbed[0] == 0 && n == 1{
        return true
    }

    if NumOfthrice>=n { return true;}
    return false;
}
```
