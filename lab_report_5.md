# Lab 5 Lab Report

## Initial EdStem post

**What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?**

I'm on a Mac, writing code in VSCode, compiling and running on zsh terminal.

**Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.**

I'm writing a method that clears all items from an ArrayList. However, it doesn't seem to be working. It leaves some items of the ArrayList behind for some reason.

Actual output:
```
javac clear.java; java clear
[world, yakuhai]
```

Expected output:
```
javac clear.java; java clear
[]
```

**Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.**

My code:

```java
import java.util.ArrayList;
public class clear {
    public static void main(String[] args) {
        ArrayList<String> myList = new ArrayList<String>();
        myList.add("hello");
        myList.add("world");
        myList.add("cse15l");
        myList.add("yakuhai");

        clearList(myList);
        System.out.println(myList.toString());
    }

    public static void clearList(ArrayList<?> list) {
        for(int i = 0; i < list.size(); i++) {
            list.remove(i);
        }
    }
}
```

I'm not really sure why it's not working. It's just using a simple for loop to loop over the ArrayList, removing the items at every index.

## TA response

Try printing out a couple things for each iteration of the for loop:

1) The current index
2) The size of the list
3) The current list

Hope this will help!

## Student response

Debugging output:

```
javac clear.java; java clear
index: 0; size: 3; current list: [world, cse15l, yakuhai]
index: 1; size: 2; current list: [world, yakuhai]
[world, yakuhai]
```

The reason why the code was failing was because the size of the list was changing as removals were happening. So, the loop was only running twice, not four times as expected.

To fix the method, first I saved the size of the list before any removals happened. Then, the loop executes that many times, removing the first item in the list rather than the i-th.

Fixed output:

```
javac clear.java; java clear
[]
```

Fixed code:

```java
import java.util.ArrayList;
public class clear {
    public static void main(String[] args) {
        ArrayList<String> myList = new ArrayList<String>();
        myList.add("hello");
        myList.add("world");
        myList.add("cse15l");
        myList.add("yakuhai");

        clearList(myList);
        System.out.println(myList.toString());
    }

    public static void clearList(ArrayList<?> list) {
        int listSize = list.size();
        for(int i = 0; i < listSize; i++) {
            list.remove(0);
        }
    }
}
```
