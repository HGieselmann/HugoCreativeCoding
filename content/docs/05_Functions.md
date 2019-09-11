You actually know a lo t about methods already. We have been using them all along, yet now we will start creating our own. In methods you can bundle together lines of code that belong logically together. They are very helpful when you need to reuse those lines a lot but they are also helpful for structuring your code. Methods also take arguments and use them in their code-block. But let’s not get ahead of ourselves and look at a very simple function:
{{<highlight c>}}
void SayHello(){
	Debug.Log(”Hello”);
}
{{</highlight>}}
Now if you would run this code nothing would happen. We only created some reusable piece of code. We need to “call” a function to actually run it:
{{<highlight c>}}
SayHello();
SayHello();
SayHello();
{{</highlight>}}
This would print “Hello” to the console three times. But let’s take a look at the syntax of defining a function again. The `void` keyword is the return-type, meaning nothing. If you want the method to return a value you would start with the type to return. Next you give your function an descriptive name and finish it with brackets.
Those brackets hold the arguments for you function, if it need them:
{{<highlight c>}}
int Add(int a, int b){
	return a + b
}
int sum;
sum = Add(5 + 5);
Debug.Log(sum);
{{</highlight>}}
Here we define a method which takes two integers and returns their sum. Now we can start using this function over and over again to add two values together. 
Now all of this is rather simplistic, so let’s take look at how we could take this into action. We will create a function, which takes an GameObject and shifts the color by a value we can also specify.
{{<highlight c >}}
void ShiftColor(float shiftValue){
            float h, s, v;
            Color oldColor = GetComponent<Renderer>().material.color;
            Color.RGBToHSV(oldColor, out h, out s, out v);
            h += shiftValue;
            if(h > 1){
                h -= 1;
            }
            Color newColor = Color.HSVToRGB(h, s, v);
            GetComponent<Renderer>().material.color = newColor;
    }
{{</highlight>}}
You know the code for changing the color already, so just take note of method we are creating. We start again with void, because we handle everything inside the method. We chose a name for our method and then give it a float value as argument. Now we can change the amount of shift each time we invoke the method. Or we could have the shift depend on the Key we press:
{{<highlight c >}}
if (Input.GetKeyDown(KeyCode.A))
        {
            ShiftColor(0.05f);
        }
        if (Input.GetKeyDown(KeyCode.S))
        {
            ShiftColor(0.1f);
        }
        if (Input.GetKeyDown(KeyCode.D))
        {
            ShiftColor(0.5f);
        }
{{</highlight>}}


- Discussion of Randomness
- animated Radomness
- recreate an image each touch
-  Sprematism
- can we implement design rules to get “non random results”

