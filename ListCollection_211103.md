# List Collection
## Last modification 21/11/03
<br>

This a list of Strings.
```Java
    List<String> colors = new List<String>();
```

Alternatively you can use an array of string to do the same.
```Java
    String[] colors = new List<String>();
```

To add elements to the list you just need:
```Java
    // Create a list and add elements to it in one step
    List<String> colors = new List<String> { 'red', 'green', blue'};
    // Add elements to a list after it has been created
    List<String> moreColors = new List<String>();
    moreColors.add('orange');
    moreColors.add('purple');
```

This elements can be readed with ***get()***, and to print all we need a bucle.
```Java
    // Get elements from a list
    String color1 = moreColors.get(0);
    String color2 = moreColors[0];
    System.assertEquals(color1, color2);
    
    // Iterate over a list to read elements
    for(Integer i=0;i<colors.size();i++) {
        // Write value to the debug log
        System.debug(colors[i]);
    }
```