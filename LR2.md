Lab Report 2 - Servers and Bugs
---

Part One:
---
Created a web server called StringServer that supports the path and behavior described. It should keep track of a single string that gets added to by incoming requests. The request will be `/add-message?s=<string>`

This certain serve should be able to do the following:


![Image](contain.png)

in order to sucessfully complete this:\
1.Go to Visual Studio Code and open a file titled as "Wavlet" or a resporitory and unzip it\
2.Create a new file and name it however youll like mine is titled "StringServer.java" (make sure it is a java file (add the .java at the end))\
3.Code in order to succesffully print out the query will look something like this

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String text = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(text);
        }
        else if (url.getPath().equals("/add-message")) {
            String message = url.getQuery();                   \\will get the Query after the path
            String messageQuery = message.substring(2);        \\Gets the second third index of the Query (so the string after the "=")
            text = text + "\n" + messageQuery;               \\will print the message of previous text and a new line with the text that will be next
            //System.out.println(text);
            return String.format(text);        \\return the string of the text
        } 
        return "404 Not Found";   \\else will say it did not find it 
    
    }
}


class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

4. Acessing the web server

**In the terminal use the commands of**

```
javac StringServer.java \\use name of your file
java StringServer 8989 \\write down any four numbers youll like
```

5. A link will pop up and will take you to the webserver youll be implementing of the Strings

![Image](url.png)

**NOTE:**
for the screenshot above the method `handleRequest(URI url)` is being called, which has an argument of a url that 
will allow the server to creat a web link and as you can see above the last section of the url which is `s=love` will be taking that string `love` and print it out just like the screen shot that follows:

**if I input some string after the path it will be formatted something like this:**

In the link above `http://localhost:8989/add-message?s=love` the path being `add-message` and the query(?) that will have `s=` ,which anything after will be whats printed
which in this case is the word `love`

![Image](print.png)


**Once you input your a string multiple times it may print out something like this (mine prints twice lol still cant figure out why (may go to OH)):** 

this is when the method `handleRequest` has taken the path message implemented to print out and if you continue to implement different strings it will have a new line be autimatically added after

**FOR EXAMPLE: if I implement this in the url**

![Image](yo.png)          **AND**        ![Image](self.png)


**IT WILL HAVE THIS PRINT OUT ( notice how self and the following strings I implemented are all after the `s=`)**

![Image](full.png)


Part Two:
---
Considering the first method in lab 3:

The following code is suppose to reverse a list to the proper formating of a reversed list, however an issue occurs where the last index of the array isnt updated to the first index (1,4,8 actually comes out as 8,4,8 instead of 8,4,1) For Example:

1. A failure inducing input for the testReverseInPlace method:

My Test Case for the method:
```
public void testReverseInPlace() {
    int[] input1 = {1, 2, 3};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[] { 3, 2, 1}, input1); //My test that didnt work 
```
![Image](failedtest.png)

2. An input that doesnt induce a failure:

My Test Case for the method that doesnt fail:
```
public void testReverseInPlace() {
    int[] input1 = {1, 2, 3};
    ArrayExamples.reverseInPlace(input1);

    assertArrayEquals(new int[] {3, 2, 3}, input1); //test that doesnt produce failure
```
![Image](passtest.png)

3. The Symptom, as the output of the following two tests above:

![Image](testoutput.png)


4. The bug(code)

looked something like this before the fix:\
```
static void reverseInPlace(int[] arr) {
    int[] temp = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
    arr = temp;
  }
```

*The code before any fixes would get the first index of the array and adjust it to the last index element, however will not adjust the last element and instead have the last element remain the same as it was oringally. Making the reverse method not expect the right pattern.

lookedlike this after the fix:\
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i -1] = temp;
    }
  }

```

*The code now will only take half of the loop and had the variable temp store the index of the first index in the array and have that value added in the last element in the array


Part Three:
---

One thing I learned from labe 2 is the whole set up itself of GitHub. I first had no clue how GitHub worked or what it was even for. Majority of the professors I have had in the past quarters Would have their own GitHub page and I as a student will easily access the code they want their students to work on. I am so fascinated about the structure of creating a resporitory and how much thought/work it takes to implement in making a new page or even the amount of detail it takes to explain one concept.
