# Output and Input

## Output

To get an output or a `console.log` (javascript) we use `System.out.println()`

```java
System.out.println("Hello World");
```

`println` means print then add a line break. If you don't want to use a line break you can simply use `print`.

```java
System.out.print("Hello ");
System.out.print("World")
```

We also can use variables in place of the string.



## Input

To get an input we have to use something called a `Scanner`. In order to use the scanner we first need to import it (unless it auto imports). Then we need to instantiate and declare a new Scanner. This looks as below

```java
package me.jaredg;

import java.util.Scanner; // could auto add this line

public class Main {
  public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
  }
}
```

After importing and creating the `scanner` variable we we can finally use it to read the users input. 

## Example of Both

Below is an example of a program using input and output.

```java
package me.jaredg;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Type in your Username?!");
        String input = scanner.nextLine();

        System.out.println("Your Username is: " + input);
    }
}
```



